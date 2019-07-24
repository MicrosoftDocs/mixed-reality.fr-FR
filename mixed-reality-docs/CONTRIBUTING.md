---
title: Instructions de contribution
description: Comment contribuer à la documentation de Windows Mixed Reality.
author: mattwojo
ms.author: mattwoj
ms.date: 03/21/2018
ms.topic: article
ms.openlocfilehash: c110b549603f42ec03fd6c0dc8df7bf70ba5ba9f
ms.sourcegitcommit: 915d3cc63a5571ba22ac4608589f3eca8da1bc81
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63516232"
---
# <a name="contributing-to-windows-mixed-reality-developer-documentation"></a><span data-ttu-id="cfb66-103">Contribution à la documentation Windows Mixed Reality Developer</span><span class="sxs-lookup"><span data-stu-id="cfb66-103">Contributing to Windows Mixed Reality developer documentation</span></span>

<span data-ttu-id="cfb66-104">Bienvenue dans la [documentation du développeur référentiel pour Windows Mixed Reality](https://github.com/MicrosoftDocs/mixed-reality/tree/master/mixed-reality-docs).</span><span class="sxs-lookup"><span data-stu-id="cfb66-104">Welcome to the [public repo for Windows Mixed Reality developer documentation](https://github.com/MicrosoftDocs/mixed-reality/tree/master/mixed-reality-docs)!</span></span> <span data-ttu-id="cfb66-105">Tous les articles que vous créez ou modifiez dans ce référentiel **seront visibles par le public.**</span><span class="sxs-lookup"><span data-stu-id="cfb66-105">Any articles you create or edit in this repo **will be visible to the public.**</span></span> 

<span data-ttu-id="cfb66-106">Les documents Windows Mixed Reality se trouvent désormais sur la plateforme docs.microsoft.com, qui utilise la démarque GitHub (avec les fonctionnalités Markdig).</span><span class="sxs-lookup"><span data-stu-id="cfb66-106">Windows Mixed Reality docs are now on the docs.microsoft.com platform, which uses GitHub-flavored Markdown (with Markdig features).</span></span> <span data-ttu-id="cfb66-107">Fondamentalement, le contenu que vous modifiez dans ce référentiel est converti en pages mises en forme et stylisées qui https://docs.microsoft.com/windows/mixed-reality s’affichent dans.</span><span class="sxs-lookup"><span data-stu-id="cfb66-107">Essentially, the content you edit in this repo gets turned into formatted and stylized pages that show up at https://docs.microsoft.com/windows/mixed-reality.</span></span> 

<span data-ttu-id="cfb66-108">Cette page présente les étapes et les instructions de base pour la contribution, ainsi que des liens vers les concepts de base de la marque.</span><span class="sxs-lookup"><span data-stu-id="cfb66-108">This page covers the basic steps and guidelines for contributing, as well as links to Markdown basics.</span></span> <span data-ttu-id="cfb66-109">Merci pour votre contribution!</span><span class="sxs-lookup"><span data-stu-id="cfb66-109">Thank you for your contribution!</span></span>

## <a name="before-you-start"></a><span data-ttu-id="cfb66-110">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="cfb66-110">Before you start</span></span>

<span data-ttu-id="cfb66-111">Si vous n’en avez pas déjà un, vous devez [créer un compte GitHub](https://github.com/join).</span><span class="sxs-lookup"><span data-stu-id="cfb66-111">If you don't already have one, you'll need to [create a GitHub account](https://github.com/join).</span></span>

>[!NOTE]
><span data-ttu-id="cfb66-112">Si vous êtes un employé de Microsoft, liez votre compte GitHub à votre alias Microsoft sur le [portail Open source de Microsoft](https://repos.opensource.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="cfb66-112">If you're a Microsoft employee, link your GitHub account to your Microsoft alias on the [Microsoft Open Source portal](https://repos.opensource.microsoft.com/).</span></span> <span data-ttu-id="cfb66-113">Rejoignez les organisations **«Microsoft»** et **«MicrosoftDocs»** ).</span><span class="sxs-lookup"><span data-stu-id="cfb66-113">Join the **"Microsoft"** and **"MicrosoftDocs"** organizations).</span></span>

<span data-ttu-id="cfb66-114">Lors de la configuration de votre compte GitHub, nous vous recommandons également les précautions de sécurité suivantes:</span><span class="sxs-lookup"><span data-stu-id="cfb66-114">When setting up your GitHub account, we also recommend these security precautions:</span></span>
- <span data-ttu-id="cfb66-115">Créez un [mot de passe fort pour votre compte GitHub](https://github.com/settings/admin).</span><span class="sxs-lookup"><span data-stu-id="cfb66-115">Create a [strong password for your Github account](https://github.com/settings/admin).</span></span>
- <span data-ttu-id="cfb66-116">Activez [l’authentification à deux facteurs](https://github.com/settings/two_factor_authentication/configure).</span><span class="sxs-lookup"><span data-stu-id="cfb66-116">Enable [two-factor authentication](https://github.com/settings/two_factor_authentication/configure).</span></span>
- <span data-ttu-id="cfb66-117">Enregistrez vos [codes de récupération](https://github.com/settings/auth/recovery-codes) dans un endroit sûr.</span><span class="sxs-lookup"><span data-stu-id="cfb66-117">Save your [recovery codes](https://github.com/settings/auth/recovery-codes) in a safe place.</span></span>
- <span data-ttu-id="cfb66-118">Mettez à jour vos [paramètres de profil public](https://github.com/settings/profile).</span><span class="sxs-lookup"><span data-stu-id="cfb66-118">Update your [public profile settings](https://github.com/settings/profile).</span></span>
   - <span data-ttu-id="cfb66-119">Définissez votre nom et envisagez de configurer votre adresse de messagerie *publique* pour *ne pas afficher mon adresse de messagerie*.</span><span class="sxs-lookup"><span data-stu-id="cfb66-119">Set your name, and consider setting your *Public email* to *Don't show my email address*.</span></span>
   - <span data-ttu-id="cfb66-120">Nous vous recommandons de télécharger une photo de profil, car une miniature s’affichera sur les pages docs auxquelles vous contribuez.</span><span class="sxs-lookup"><span data-stu-id="cfb66-120">We recommend you upload a profile picture, as a thumbnail will be shown on docs pages to which you contribute.</span></span>
- <span data-ttu-id="cfb66-121">Si vous envisagez d’utiliser un flux de travail de ligne de commande, pensez à configurer [git Credential Manager pour Windows](https://github.com/Microsoft/Git-Credential-Manager-for-Windows/releases/latest) afin de ne pas avoir à entrer votre mot de passe chaque fois que vous effectuez une contribution.</span><span class="sxs-lookup"><span data-stu-id="cfb66-121">If you plan to use a command line workflow, consider setting up [Git Credential Manager for Windows](https://github.com/Microsoft/Git-Credential-Manager-for-Windows/releases/latest) so that you don't have to enter your password each time you make a contribution.</span></span>

<span data-ttu-id="cfb66-122">La réalisation de ces étapes est importante, car le système de publication est lié à GitHub et vous êtes mentionné comme auteur ou contributeur à chaque article à l’aide de votre alias GitHub.</span><span class="sxs-lookup"><span data-stu-id="cfb66-122">Taking these steps is important, as the publishing system is tied to GitHub and you'll be listed as either author or contributor to each article using your GitHub alias.</span></span>

## <a name="editing-an-existing-article"></a><span data-ttu-id="cfb66-123">Modification d’un article existant</span><span class="sxs-lookup"><span data-stu-id="cfb66-123">Editing an existing article</span></span>

<span data-ttu-id="cfb66-124">Utilisez le flux de travail suivant pour effectuer des mises à jour d' *un article existant* via github dans un navigateur Web:</span><span class="sxs-lookup"><span data-stu-id="cfb66-124">Use the following workflow to make updates to *an existing article* via GitHub in a web browser:</span></span>

1. <span data-ttu-id="cfb66-125">Accédez à l’article que vous souhaitez modifier dans le dossier «Mixed-Real-docs».</span><span class="sxs-lookup"><span data-stu-id="cfb66-125">Navigate to the article you wish to edit in the "mixed-reality-docs" folder.</span></span>
2. <span data-ttu-id="cfb66-126">Cliquez sur le bouton modifier (icône crayon) dans le coin supérieur droit.</span><span class="sxs-lookup"><span data-stu-id="cfb66-126">Select the edit button (pencil icon) in the top right.</span></span> <span data-ttu-id="cfb66-127">Cela permet de dupliquer automatiquement une branche jetable en dehors de la branche «master».</span><span class="sxs-lookup"><span data-stu-id="cfb66-127">This will automatically fork a disposable branch off the 'master' branch.</span></span>

   ![Modifier un article.](images/editpage.png)
3. <span data-ttu-id="cfb66-129">Modifiez le contenu de l’article (consultez [«principes de base](#markdown-basics) des démarques» ci-dessous pour obtenir de l’aide).</span><span class="sxs-lookup"><span data-stu-id="cfb66-129">Edit the content of the article (see ["Markdown basics"](#markdown-basics) below for guidance).</span></span>
4. <span data-ttu-id="cfb66-130">Mettez à jour les métadonnées en haut de chaque article:</span><span class="sxs-lookup"><span data-stu-id="cfb66-130">Update metadata as relevant at the top of each article:</span></span>
   * <span data-ttu-id="cfb66-131">bonhomme Il s’agit du titre de la page qui s’affiche sous l’onglet navigateur lorsque l’article est affiché.</span><span class="sxs-lookup"><span data-stu-id="cfb66-131">title: This is the page title that appears in the browser tab when the article is being viewed.</span></span> <span data-ttu-id="cfb66-132">Comme il est utilisé pour le SEO et l’indexation, vous ne devez pas modifier le titre sauf si cela est nécessaire (bien que cela soit moins critique avant que la documentation ne soit publique).</span><span class="sxs-lookup"><span data-stu-id="cfb66-132">As this is used for SEO and indexing, you shouldn't change the title unless necessary (though this is less critical before documentation goes public).</span></span>
   * <span data-ttu-id="cfb66-133">Descriptive Rédigez une brève description du contenu de l’article.</span><span class="sxs-lookup"><span data-stu-id="cfb66-133">description: Write a brief description of the article's content.</span></span> <span data-ttu-id="cfb66-134">Cela facilite la découverte et le SEO.</span><span class="sxs-lookup"><span data-stu-id="cfb66-134">This aids in SEO and discovery.</span></span>
   * <span data-ttu-id="cfb66-135">auteur Si vous êtes le propriétaire principal de la page, ajoutez votre alias GitHub ici.</span><span class="sxs-lookup"><span data-stu-id="cfb66-135">author: If you are the primary owner of the page, add your GitHub alias here.</span></span>
   * <span data-ttu-id="cfb66-136">ms. Author: Si vous êtes le propriétaire principal de la page, ajoutez votre alias Microsoft ici (vous n’en @microsoft.comavez pas besoin, juste l’alias).</span><span class="sxs-lookup"><span data-stu-id="cfb66-136">ms.author: If you are the primary owner of the page, add your Microsoft alias here (you don't need @microsoft.com, just the alias).</span></span>
   * <span data-ttu-id="cfb66-137">ms. Date: Mettez à jour la date si vous ajoutez du contenu majeur à la page, mais pas pour des correctifs tels que la clarification, la mise en forme, la grammaire ou l’orthographe.</span><span class="sxs-lookup"><span data-stu-id="cfb66-137">ms.date: Update the date if you're adding major content to the page, but not for fixes like clarification, formatting, grammar, or spelling.</span></span>
   * <span data-ttu-id="cfb66-138">mot Les mots clés aident dans SEO (optimisation du moteur de recherche).</span><span class="sxs-lookup"><span data-stu-id="cfb66-138">keywords: Keywords aid in SEO (search engine optimization).</span></span> <span data-ttu-id="cfb66-139">Ajoutez des mots clés, séparés par une virgule et un espace, qui sont spécifiques à votre article (mais aucune ponctuation après le dernier mot clé de votre liste). vous n’avez pas besoin d’ajouter des mots clés globaux qui s’appliquent à tous les articles, car ceux-ci sont gérés ailleurs.</span><span class="sxs-lookup"><span data-stu-id="cfb66-139">Add keywords, separated by a comma and a space, that are specific to your article (but no punctuation after the last keyword in your list); you don't need to add global keywords that apply to all articles, as those are managed elsewhere.</span></span> 
5. <span data-ttu-id="cfb66-140">Une fois que vous avez terminé vos modifications, faites défiler la liste et cliquez sur le bouton **proposer un changement de fichier** .</span><span class="sxs-lookup"><span data-stu-id="cfb66-140">When you've completed your article edits, scroll down and click the **Propose file change** button.</span></span>
6. <span data-ttu-id="cfb66-141">Sur la page suivante, cliquez sur **créer une demande de tirage (pull Request** ) pour fusionner votre branche créée automatiquement dans «Master».</span><span class="sxs-lookup"><span data-stu-id="cfb66-141">On the next page, click **Create pull request** to merge your automatically-created branch into 'master.'</span></span>
7. <span data-ttu-id="cfb66-142">Répétez les étapes ci-dessus pour le prochain article que vous souhaitez modifier.</span><span class="sxs-lookup"><span data-stu-id="cfb66-142">Repeat the steps above for the next article you want to edit.</span></span>

## <a name="creating-a-new-article"></a><span data-ttu-id="cfb66-143">Création d’un article</span><span class="sxs-lookup"><span data-stu-id="cfb66-143">Creating a new article</span></span>

<span data-ttu-id="cfb66-144">Utilisez le flux de travail suivant pour *créer de nouveaux articles* dans la documentation référentiel via github dans un navigateur Web:</span><span class="sxs-lookup"><span data-stu-id="cfb66-144">Use the following workflow to *create new articles* in the documentation repo via GitHub in a web browser:</span></span>

1. <span data-ttu-id="cfb66-145">Créez une fourche à partir de la branche «master» MicrosoftDocs/de la réalité mixte (à l’aide du bouton de **branchement** dans le coin supérieur droit).</span><span class="sxs-lookup"><span data-stu-id="cfb66-145">Create a fork off the MicrosoftDocs/mixed-reality 'master' branch (using the **Fork** button in the top right).</span></span>

   ![Dupliquez la branche principale.](images/forkbranch.png)
2. <span data-ttu-id="cfb66-147">Dans le dossier «Mixed-Real-docs», cliquez sur le bouton **créer un fichier** dans le coin supérieur droit.</span><span class="sxs-lookup"><span data-stu-id="cfb66-147">In the "mixed-reality-docs" folder, click the **Create new file** button in the top right.</span></span>
3. <span data-ttu-id="cfb66-148">Créer un nom de page pour l’article (utilisez des traits d’Union à la place d’espaces et n’utilisez pas de ponctuation ou d’apostrophes) et ajoutez «. MD»</span><span class="sxs-lookup"><span data-stu-id="cfb66-148">Create a page name for the article (use hyphens instead of spaces and don't use punctuation or apostrophes) and append ".md"</span></span>

   ![Nommez votre nouvelle page.](images/newpagetitle.PNG)
   
   >[!IMPORTANT]
   ><span data-ttu-id="cfb66-150">Veillez à créer le nouvel article dans le dossier «Mixed-Real-docs».</span><span class="sxs-lookup"><span data-stu-id="cfb66-150">Make sure you create the new article from within the "mixed-reality-docs" folder.</span></span> <span data-ttu-id="cfb66-151">Vous pouvez le vérifier en recherchant «/Mixed-Reality-docs/» dans la ligne du nouveau nom de fichier.</span><span class="sxs-lookup"><span data-stu-id="cfb66-151">You can confirm this by checking for "/mixed-reality-docs/" in the new file name line.</span></span>

4. <span data-ttu-id="cfb66-152">En haut de votre nouvelle page, ajoutez le bloc de métadonnées suivant:</span><span class="sxs-lookup"><span data-stu-id="cfb66-152">At the top of your new page, add the following metadata block:</span></span>

   ```md
   ---
   title:
   description:
   author:
   ms.author:
   ms.date:
   ms.topic: article
   keywords:
   ---
   ```

5. <span data-ttu-id="cfb66-153">Renseignez les champs de métadonnées pertinents conformément aux instructions de la [section ci-dessus](#editing-an-existing-article).</span><span class="sxs-lookup"><span data-stu-id="cfb66-153">Fill in the relevant metadata fields per the instructions in the [section above](#editing-an-existing-article).</span></span>
6. <span data-ttu-id="cfb66-154">Écrivez le contenu de l’article à l’aide des [principes fondamentaux](#markdown-basics).</span><span class="sxs-lookup"><span data-stu-id="cfb66-154">Write article content using [Markdown basics](#markdown-basics).</span></span>
7. <span data-ttu-id="cfb66-155">Ajoutez une `## See also` section au bas de l’article avec des liens vers d’autres articles pertinents.</span><span class="sxs-lookup"><span data-stu-id="cfb66-155">Add a `## See also` section at the bottom of the article with links to other relevant articles.</span></span>
8. <span data-ttu-id="cfb66-156">Lorsque vous avez terminé, cliquez sur **valider le nouveau fichier**.</span><span class="sxs-lookup"><span data-stu-id="cfb66-156">When finished, click **Commit new file**.</span></span>
9. <span data-ttu-id="cfb66-157">Cliquez sur **nouvelle demande de tirage (pull Request** ) et fusionnez la branche’Master’de votre branche dans MicrosoftDocs/Mixed-Reality’Master' (Assurez-vous que la flèche pointe vers la bonne voie).</span><span class="sxs-lookup"><span data-stu-id="cfb66-157">Click **New pull request** and merge your fork's 'master' branch into MicrosoftDocs/mixed-reality 'master' (make sure the arrow is pointing the correct way).</span></span>

   ![Créer une requête de tirage (pull request) à partir de votre fourche dans MicrosoftDocs/Mixed-Reality](images/pr_to_master.PNG)

## <a name="markdown-basics"></a><span data-ttu-id="cfb66-159">Notions de base de la démarque</span><span class="sxs-lookup"><span data-stu-id="cfb66-159">Markdown basics</span></span>

<span data-ttu-id="cfb66-160">Les ressources suivantes vous permettront d’apprendre à modifier la documentation à l’aide du langage de démarque:</span><span class="sxs-lookup"><span data-stu-id="cfb66-160">The following resources will help you learn how to edit documentation using the Markdown language:</span></span>

- [<span data-ttu-id="cfb66-161">Notions de base de la démarque</span><span class="sxs-lookup"><span data-stu-id="cfb66-161">Markdown basics</span></span>](https://help.github.com/articles/basic-writing-and-formatting-syntax/)
- [<span data-ttu-id="cfb66-162">Affiche de référence de démarque-en un clin d’œil</span><span class="sxs-lookup"><span data-stu-id="cfb66-162">Markdown-at-a-glance reference poster</span></span>](images/MarkdownPoster.pdf)
- [<span data-ttu-id="cfb66-163">Ressources supplémentaires pour l’écriture de la démarque pour docs.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="cfb66-163">Additional resources for writing Markdown for docs.microsoft.com</span></span>](https://docs.microsoft.com/contribute/how-to-write-use-markdown)

### <a name="adding-tables"></a><span data-ttu-id="cfb66-164">Ajout de tables</span><span class="sxs-lookup"><span data-stu-id="cfb66-164">Adding tables</span></span>

<span data-ttu-id="cfb66-165">En raison de la façon dont les tableaux de styles docs.microsoft.com, ils n’ont pas de bordures ou de styles personnalisés, même si vous essayez le style CSS en ligne.</span><span class="sxs-lookup"><span data-stu-id="cfb66-165">Because of the way docs.microsoft.com styles tables, they won’t have borders or custom styles, even if you try inline CSS.</span></span> <span data-ttu-id="cfb66-166">Il semblera fonctionner pendant une période de temps limitée, mais la plateforme finira par supprimer le style de la table.</span><span class="sxs-lookup"><span data-stu-id="cfb66-166">It will appear to work for a short period of time, but eventually the platform will strip the styling out of the table.</span></span> <span data-ttu-id="cfb66-167">Vous devez donc anticiper et garder vos tables simples.</span><span class="sxs-lookup"><span data-stu-id="cfb66-167">So plan ahead and keep your tables simple.</span></span> <span data-ttu-id="cfb66-168">[Voici un site qui](http://www.tablesgenerator.com/markdown_tables)simplifie les tableaux de démarques.</span><span class="sxs-lookup"><span data-stu-id="cfb66-168">[Here’s a site that makes Markdown tables easy](http://www.tablesgenerator.com/markdown_tables).</span></span>

<span data-ttu-id="cfb66-169">L' [extension docs de démarque pour Visual Studio code](https://docs.microsoft.com/teamblog/docs-extension) facilite également la génération de table si vous utilisez [Visual Studio code (voir ci-dessous)](#using-visual-studio-code) pour modifier la documentation.</span><span class="sxs-lookup"><span data-stu-id="cfb66-169">The [Docs Markdown Extension for Visual Studio Code](https://docs.microsoft.com/teamblog/docs-extension) also makes table generation easy if you're using [Visual Studio Code (see below)](#using-visual-studio-code) to edit the documentation.</span></span>

### <a name="adding-images"></a><span data-ttu-id="cfb66-170">Ajouter des images</span><span class="sxs-lookup"><span data-stu-id="cfb66-170">Adding images</span></span>

<span data-ttu-id="cfb66-171">Vous devez charger vos images dans le dossier «Mixed-Real-docs/images» dans référentiel, puis les référencer de manière appropriée dans l’article.</span><span class="sxs-lookup"><span data-stu-id="cfb66-171">You’ll need to upload your images to the "mixed-reality-docs/images" folder in the repo, and then reference them appropriately in the article.</span></span> <span data-ttu-id="cfb66-172">Les images s’affichent automatiquement à la taille maximale, ce qui signifie que si votre image est volumineuse, elle remplit toute la largeur de l’article.</span><span class="sxs-lookup"><span data-stu-id="cfb66-172">Images will automatically show up at full-size, which means if your image is large, it’ll fill the entire width of the article.</span></span> <span data-ttu-id="cfb66-173">Par conséquent, nous vous recommandons de prédimensionner vos images avant de les charger.</span><span class="sxs-lookup"><span data-stu-id="cfb66-173">Thus, we recommend pre-sizing your images before uploading them.</span></span> <span data-ttu-id="cfb66-174">La largeur recommandée est comprise entre 600 et 700 pixels, même si vous devez monter ou diminuer la taille s’il s’agit d’une capture d’écran dense ou d’une fraction d’une capture d’écran, respectivement.</span><span class="sxs-lookup"><span data-stu-id="cfb66-174">The recommended width is between 600 and 700 pixels, though you should size up or down if it’s a dense screenshot or a fraction of a screenshot, respectively.</span></span>

>[!IMPORTANT]
><span data-ttu-id="cfb66-175">Vous pouvez uniquement charger des images sur vos référentiel dupliqués avant la fusion.</span><span class="sxs-lookup"><span data-stu-id="cfb66-175">You can only upload images to your forked repo before merging.</span></span> <span data-ttu-id="cfb66-176">Par conséquent, si vous envisagez d’ajouter des images à un article, vous devez [utiliser Visual Studio code](#using-visual-studio-code) pour ajouter d’abord les images au dossier «images» de votre branche, ou vous assurer que vous avez effectué les opérations suivantes dans un navigateur Web:</span><span class="sxs-lookup"><span data-stu-id="cfb66-176">So, if you plan on adding images to an article, you'll need to [use Visual Studio Code](#using-visual-studio-code) to add the images to your fork's "images" folder first or make sure you've done the following in a web browser:</span></span>
>
>1. <span data-ttu-id="cfb66-177">A fait la duplication du référentiel MicrosoftDocs/Mixed-Reality.</span><span class="sxs-lookup"><span data-stu-id="cfb66-177">Forked the MicrosoftDocs/mixed-reality repo.</span></span>
>2. <span data-ttu-id="cfb66-178">Modification de l’article dans votre fourche.</span><span class="sxs-lookup"><span data-stu-id="cfb66-178">Edited the article in your fork.</span></span>
>3. <span data-ttu-id="cfb66-179">Téléchargez les images que vous référencez dans votre article dans le dossier «Mixed-Real-docs/images» de votre fourche.</span><span class="sxs-lookup"><span data-stu-id="cfb66-179">Uploaded the images you're referencing in your article to the "mixed-reality-docs/images" folder in your fork.</span></span>
>4. <span data-ttu-id="cfb66-180">Création d’une **requête de tirage** pour fusionner votre fourche dans la branche «master» MicrosoftDocs/de la réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="cfb66-180">Created a **pull request** to merge your fork into the MicrosoftDocs/mixed-reality 'master' branch.</span></span>
>
><span data-ttu-id="cfb66-181">Pour savoir comment configurer vos propres référentiel dupliqués, suivez les instructions de création d' [un nouvel article](#creating-a-new-article).</span><span class="sxs-lookup"><span data-stu-id="cfb66-181">To learn how to set up your own forked repo, follow the instructions for [creating a new article](#creating-a-new-article).</span></span>

## <a name="previewing-your-work"></a><span data-ttu-id="cfb66-182">Aperçu de votre travail</span><span class="sxs-lookup"><span data-stu-id="cfb66-182">Previewing your work</span></span>

<span data-ttu-id="cfb66-183">Pendant la modification dans GitHub via un navigateur Web, vous pouvez cliquer sur l’onglet d' **Aperçu** en haut de la page pour afficher un aperçu de votre travail avant de le valider.</span><span class="sxs-lookup"><span data-stu-id="cfb66-183">While editing in GitHub via a web browser, you can click the **Preview** tab near the top of the page to preview your work before committing.</span></span> 

>[!NOTE]
><span data-ttu-id="cfb66-184">L’aperçu de vos modifications sur review.docs.microsoft.com n’est disponible que pour les employés de Microsoft</span><span class="sxs-lookup"><span data-stu-id="cfb66-184">Previewing your changes on review.docs.microsoft.com is only available to Microsoft employees</span></span>

<span data-ttu-id="cfb66-185">Employés de Microsoft: une fois vos contributions fusionnées dans la branche principale, vous pouvez voir à quoi ressemblera la documentation avant qu’elle ne soit publique https://review.docs.microsoft.com/windows/mixed-reality?branch=master (recherchez votre article à l’aide de la table des matières dans la colonne de gauche).</span><span class="sxs-lookup"><span data-stu-id="cfb66-185">Microsoft employees: once your contributions have been merged into the 'master' branch, you can see what the documentation will look like before it goes public at https://review.docs.microsoft.com/windows/mixed-reality?branch=master (find your article using the table of contents in the left column).</span></span>

## <a name="editing-in-the-browser-vs-editing-with-a-desktop-client"></a><span data-ttu-id="cfb66-186">Modification dans le navigateur et modification avec un client Desktop</span><span class="sxs-lookup"><span data-stu-id="cfb66-186">Editing in the browser vs. editing with a desktop client</span></span>

<span data-ttu-id="cfb66-187">La modification dans le navigateur est le moyen le plus simple pour apporter des modifications rapides, toutefois, il existe quelques inconvénients:</span><span class="sxs-lookup"><span data-stu-id="cfb66-187">Editing in the browser is the easiest way to make quick changes, however, there are a few disadvantages:</span></span>

- <span data-ttu-id="cfb66-188">Vous n’avez pas de vérification orthographique.</span><span class="sxs-lookup"><span data-stu-id="cfb66-188">You don't get spell-check.</span></span>
- <span data-ttu-id="cfb66-189">Vous n’avez pas de lien intelligent vers d’autres articles (vous devez taper manuellement le nom de fichier de l’article).</span><span class="sxs-lookup"><span data-stu-id="cfb66-189">You don't get any smart-linking to other articles (you have to manually type the article's filename).</span></span>
- <span data-ttu-id="cfb66-190">Il peut être laborieux de charger et de référencer des images.</span><span class="sxs-lookup"><span data-stu-id="cfb66-190">It can be a hassle to upload and reference images.</span></span>

<span data-ttu-id="cfb66-191">Si vous préférez ne pas traiter ces problèmes, vous préférerez peut-être utiliser un client de bureau comme [Visual Studio code](https://code.visualstudio.com/) avec quelques [Extensions utiles](#useful-extensions) pour contribuer à la documentation.</span><span class="sxs-lookup"><span data-stu-id="cfb66-191">If you'd rather not deal with these issues, you may prefer to use a desktop client like [Visual Studio Code](https://code.visualstudio.com/) with a couple [helpful extensions](#useful-extensions) to contribute to documentation.</span></span>

## <a name="using-visual-studio-code"></a><span data-ttu-id="cfb66-192">Utilisation de Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="cfb66-192">Using Visual Studio Code</span></span>

<span data-ttu-id="cfb66-193">Pour les raisons mentionnées [ci-dessus](#editing-in-the-browser-vs-editing-with-a-desktop-client), vous préférerez peut-être utiliser un client de bureau pour modifier la documentation au lieu d’un navigateur Web.</span><span class="sxs-lookup"><span data-stu-id="cfb66-193">For the reasons listed [above](#editing-in-the-browser-vs-editing-with-a-desktop-client), you may prefer using a desktop client to edit documentation instead of a web browser.</span></span> <span data-ttu-id="cfb66-194">Nous vous recommandons d’utiliser [Visual Studio code](https://code.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="cfb66-194">We recommend using [Visual Studio Code](https://code.visualstudio.com/).</span></span>

### <a name="setup"></a><span data-ttu-id="cfb66-195">Installation</span><span class="sxs-lookup"><span data-stu-id="cfb66-195">Setup</span></span>

<span data-ttu-id="cfb66-196">Procédez comme suit pour configurer Visual Studio Code pour qu’il fonctionne avec ce référentiel:</span><span class="sxs-lookup"><span data-stu-id="cfb66-196">Follow these steps to configure Visual Studio Code to work with this repo:</span></span>

1. <span data-ttu-id="cfb66-197">Dans un navigateur Web:</span><span class="sxs-lookup"><span data-stu-id="cfb66-197">In a web browser:</span></span>
    1. <span data-ttu-id="cfb66-198">Installez [git pour votre PC](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="cfb66-198">Install [Git for your PC](https://git-scm.com/downloads).</span></span>
    2. <span data-ttu-id="cfb66-199">Installez [Visual Studio code](https://code.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="cfb66-199">Install [Visual Studio Code](https://code.visualstudio.com/).</span></span>
    3. <span data-ttu-id="cfb66-200">[Duplication de MicrosoftDocs/Mixed-realisation](#creating-a-new-article) si vous ne l’avez pas déjà fait.</span><span class="sxs-lookup"><span data-stu-id="cfb66-200">[Fork MicrosoftDocs/mixed-reality](#creating-a-new-article) if you haven't already.</span></span>
    4. <span data-ttu-id="cfb66-201">Dans votre fourche, cliquez sur **cloner ou télécharger** et copiez l’URL.</span><span class="sxs-lookup"><span data-stu-id="cfb66-201">In your fork, click **Clone or download** and copy the URL.</span></span>
2. <span data-ttu-id="cfb66-202">Créez un clone local de votre fourche dans Visual Studio Code:</span><span class="sxs-lookup"><span data-stu-id="cfb66-202">Create a local clone of your fork in Visual Studio Code:</span></span>
    1. <span data-ttu-id="cfb66-203">Dans le menu **affichage** , sélectionnez **palette de commandes**.</span><span class="sxs-lookup"><span data-stu-id="cfb66-203">From the **View** menu, select **Command Palette**.</span></span>
    2. <span data-ttu-id="cfb66-204">Tapez «git: Clone».</span><span class="sxs-lookup"><span data-stu-id="cfb66-204">Type "Git:Clone."</span></span>
    3. <span data-ttu-id="cfb66-205">Collez l’URL que vous venez de copier.</span><span class="sxs-lookup"><span data-stu-id="cfb66-205">Paste the URL you just copied.</span></span>
    4. <span data-ttu-id="cfb66-206">Choisissez l’emplacement où enregistrer le clone sur votre PC.</span><span class="sxs-lookup"><span data-stu-id="cfb66-206">Choose where to save the clone on your PC.</span></span>
    5. <span data-ttu-id="cfb66-207">Dans la fenêtre contextuelle, cliquez sur **ouvrir référentiel** .</span><span class="sxs-lookup"><span data-stu-id="cfb66-207">Click **Open repo** in the pop-up.</span></span>

### <a name="editing-documentation"></a><span data-ttu-id="cfb66-208">Modification de la documentation</span><span class="sxs-lookup"><span data-stu-id="cfb66-208">Editing documentation</span></span>

<span data-ttu-id="cfb66-209">Utilisez le flux de travail suivant pour apporter des modifications à la documentation avec Visual Studio Code:</span><span class="sxs-lookup"><span data-stu-id="cfb66-209">Use the following workflow to make changes to the documentation with Visual Studio Code:</span></span>

>[!NOTE]
><span data-ttu-id="cfb66-210">Toutes les instructions relatives à la [modification](#editing-an-existing-article) et à la [création](#creating-a-new-article) d’articles, ainsi que les [principes fondamentaux de la modification de](#markdown-basics)la démarque, ci-dessus s’appliquent également à l’utilisation de Visual Studio code.</span><span class="sxs-lookup"><span data-stu-id="cfb66-210">All the guidance for [editing](#editing-an-existing-article) and [creating](#creating-a-new-article) articles, and the [basics of editing Markdown](#markdown-basics), from above applies when using Visual Studio Code as well.</span></span>

1. <span data-ttu-id="cfb66-211">Assurez-vous que votre fourche cloné est à jour avec la référentiel officielle.</span><span class="sxs-lookup"><span data-stu-id="cfb66-211">Make sure your cloned fork is up-to-date with the official repo.</span></span>
   1. <span data-ttu-id="cfb66-212">Dans un navigateur Web, créez une requête de tirage pour synchroniser les modifications récentes des autres contributeurs de MicrosoftDocs/Mixed-Reality’Master’sur votre fourche (Assurez-vous que la flèche pointe vers la bonne voie).</span><span class="sxs-lookup"><span data-stu-id="cfb66-212">In a web browser, create a pull request to sync recent changes from other contributors in MicrosoftDocs/mixed-reality 'master' to your fork (make sure the arrow is pointing the right way).</span></span>
      
      ![Synchroniser les modifications de MicrosoftDocs/Mixed-Reality avec votre fourche](images/sync_repos.PNG)
   2. <span data-ttu-id="cfb66-214">Dans Visual Studio Code, cliquez sur le bouton synchroniser pour synchroniser votre branche fraîchement mise à jour sur le clone local.</span><span class="sxs-lookup"><span data-stu-id="cfb66-214">In Visual Studio Code, click the sync button to sync your freshly updated fork to the local clone.</span></span>
      
      ![Cliquez sur le bouton synchroniser.](images/sync_clone.png)
2. <span data-ttu-id="cfb66-216">Créez ou modifiez des articles dans votre référentiel cloné à l’aide de Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="cfb66-216">Create or edit articles in your cloned repo using Visual Studio Code.</span></span>
   1. <span data-ttu-id="cfb66-217">Modifiez un ou plusieurs articles (ajoutez des images au dossier «images» si nécessaire).</span><span class="sxs-lookup"><span data-stu-id="cfb66-217">Edit one or more articles (add images to “images” folder if necessary).</span></span>
   2. <span data-ttu-id="cfb66-218">**Enregistrer** les modifications dans l' **Explorateur**.</span><span class="sxs-lookup"><span data-stu-id="cfb66-218">**Save** changes in **Explorer**.</span></span>
      
      ![Choisissez «Enregistrer tout» dans l’Explorateur](images/explorer_save.png)
   3. <span data-ttu-id="cfb66-220">**Valide toutes les** modifications dans **le contrôle de code source** (message de validation en écriture quand vous y êtes invité).</span><span class="sxs-lookup"><span data-stu-id="cfb66-220">**Commit all** changes in **Source Control** (write commit message when prompted).</span></span>
      
      ![Choisissez «valider tout» dans le contrôle de code source](images/source_control_commit.png)
   4. <span data-ttu-id="cfb66-222">Cliquez sur  le bouton synchroniser pour resynchroniser vos modifications avec l’origine (votre fourche sur GitHub).</span><span class="sxs-lookup"><span data-stu-id="cfb66-222">Click the **sync** button to sync your changes back to origin (your fork on GitHub).</span></span>
      
      ![Cliquez sur le bouton synchroniser.](images/sync_back.png)
3. <span data-ttu-id="cfb66-224">Dans un navigateur Web, créez une requête de tirage pour synchroniser les modifications apportées à votre fourche en MicrosoftDocs/Mixed-Reality’Master' (Assurez-vous que la flèche pointe vers la bonne voie).</span><span class="sxs-lookup"><span data-stu-id="cfb66-224">In a web browser, create a pull request to sync new changes in your fork back to MicrosoftDocs/mixed-reality 'master' (make sure the arrow is pointing the correct way).</span></span>

   ![Créer une requête de tirage (pull request) à partir de votre fourche dans MicrosoftDocs/Mixed-Reality](images/pr_to_master.PNG)

### <a name="useful-extensions"></a><span data-ttu-id="cfb66-226">Extensions utiles</span><span class="sxs-lookup"><span data-stu-id="cfb66-226">Useful extensions</span></span>

<span data-ttu-id="cfb66-227">Les extensions de Visual Studio Code suivantes sont très utiles lors de la modification de la documentation:</span><span class="sxs-lookup"><span data-stu-id="cfb66-227">The following Visual Studio Code extensions are very useful when editing documentation:</span></span>

- <span data-ttu-id="cfb66-228">[Extension docs de la marque pour Visual Studio code](https://marketplace.visualstudio.com/items?itemName=docsmsft.docs-authoring-pack) -utilisez **ALT + M** pour afficher un menu d’options de création de documents, comme:</span><span class="sxs-lookup"><span data-stu-id="cfb66-228">[Docs Markdown Extension for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=docsmsft.docs-authoring-pack) - Use **Alt+M** to bring up a menu of docs authoring options like:</span></span>
   - <span data-ttu-id="cfb66-229">Recherchez et référencez des images que vous avez téléchargées.</span><span class="sxs-lookup"><span data-stu-id="cfb66-229">Search and reference images you've uploaded.</span></span>
   - <span data-ttu-id="cfb66-230">Ajoutez une mise en forme comme des listes, des tables et des appels spécifiques aux `>[!NOTE]`documents, comme.</span><span class="sxs-lookup"><span data-stu-id="cfb66-230">Add formatting like lists, tables, and docs-specific call-outs like `>[!NOTE]`.</span></span>
   - <span data-ttu-id="cfb66-231">Recherchez et référencez des liens et des signets internes (liens vers des sections spécifiques dans une page).</span><span class="sxs-lookup"><span data-stu-id="cfb66-231">Search and reference internal links and bookmarks (links to specific sections within a page).</span></span>
   - <span data-ttu-id="cfb66-232">Les erreurs de mise en forme sont mises en surbrillance (pointez votre souris sur l’erreur pour en savoir plus).</span><span class="sxs-lookup"><span data-stu-id="cfb66-232">Formatting errors are highlighted (hover your mouse over the error to learn more).</span></span>
- <span data-ttu-id="cfb66-233">[Vérificateur orthographique de code](https://marketplace.visualstudio.com/items?itemName=streetsidesoftware.code-spell-checker) : les mots mal orthographiés sont soulignés. Cliquez avec le bouton droit sur un mot mal orthographié pour le modifier ou enregistrez-le dans le dictionnaire.</span><span class="sxs-lookup"><span data-stu-id="cfb66-233">[Code Spell Checker](https://marketplace.visualstudio.com/items?itemName=streetsidesoftware.code-spell-checker) - misspelled words will be underlined; right-click on a misspelled word to change it or save it to the dictionary.</span></span>
