---
title: Instructions de contribution
description: Comment contribuer à la documentation Windows Mixed Reality.
author: mattwojo
ms.author: mattwoj
ms.date: 03/21/2018
ms.topic: article
ms.openlocfilehash: c110b549603f42ec03fd6c0dc8df7bf70ba5ba9f
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59596945"
---
# <a name="contributing-to-windows-mixed-reality-developer-documentation"></a><span data-ttu-id="13159-103">Contribuez à la documentation de développement Windows Mixed Reality</span><span class="sxs-lookup"><span data-stu-id="13159-103">Contributing to Windows Mixed Reality developer documentation</span></span>

<span data-ttu-id="13159-104">Bienvenue dans le [référentiel public pour la documentation pour développeurs Windows Mixed Reality](https://github.com/MicrosoftDocs/mixed-reality/tree/master/mixed-reality-docs)!</span><span class="sxs-lookup"><span data-stu-id="13159-104">Welcome to the [public repo for Windows Mixed Reality developer documentation](https://github.com/MicrosoftDocs/mixed-reality/tree/master/mixed-reality-docs)!</span></span> <span data-ttu-id="13159-105">Des articles que vous créez ou modifiez dans ce dépôt **sera visible au public.**</span><span class="sxs-lookup"><span data-stu-id="13159-105">Any articles you create or edit in this repo **will be visible to the public.**</span></span> 

<span data-ttu-id="13159-106">Documentation de Windows Mixed Reality se trouve désormais sur la plateforme docs.microsoft.com, qui utilise Markdown de GitHub-flavored (avec des fonctionnalités de Markdig).</span><span class="sxs-lookup"><span data-stu-id="13159-106">Windows Mixed Reality docs are now on the docs.microsoft.com platform, which uses GitHub-flavored Markdown (with Markdig features).</span></span> <span data-ttu-id="13159-107">Essentiellement, le contenu que vous modifiez dans ce dépôt obtient transformé de pages mises en forme et stylisés qui s’affichent à https://docs.microsoft.com/windows/mixed-reality.</span><span class="sxs-lookup"><span data-stu-id="13159-107">Essentially, the content you edit in this repo gets turned into formatted and stylized pages that show up at https://docs.microsoft.com/windows/mixed-reality.</span></span> 

<span data-ttu-id="13159-108">Cette page décrit les étapes de base et les instructions pour votre contribution, ainsi que des liens vers les bases de Markdown.</span><span class="sxs-lookup"><span data-stu-id="13159-108">This page covers the basic steps and guidelines for contributing, as well as links to Markdown basics.</span></span> <span data-ttu-id="13159-109">Nous vous remercions de votre contribution.</span><span class="sxs-lookup"><span data-stu-id="13159-109">Thank you for your contribution!</span></span>

## <a name="before-you-start"></a><span data-ttu-id="13159-110">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="13159-110">Before you start</span></span>

<span data-ttu-id="13159-111">Si vous n’en avez déjà, vous devrez [créer un compte GitHub](https://github.com/join).</span><span class="sxs-lookup"><span data-stu-id="13159-111">If you don't already have one, you'll need to [create a GitHub account](https://github.com/join).</span></span>

>[!NOTE]
><span data-ttu-id="13159-112">Si vous êtes un employé de Microsoft, liez votre compte GitHub à votre alias Microsoft sur le [portail de Microsoft Open Source](https://repos.opensource.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="13159-112">If you're a Microsoft employee, link your GitHub account to your Microsoft alias on the [Microsoft Open Source portal](https://repos.opensource.microsoft.com/).</span></span> <span data-ttu-id="13159-113">Joindre le **« Microsoft »** et **« MicrosoftDocs »** organisations).</span><span class="sxs-lookup"><span data-stu-id="13159-113">Join the **"Microsoft"** and **"MicrosoftDocs"** organizations).</span></span>

<span data-ttu-id="13159-114">Lorsque vous configurez votre compte GitHub, nous vous recommandons également ces précautions de sécurité :</span><span class="sxs-lookup"><span data-stu-id="13159-114">When setting up your GitHub account, we also recommend these security precautions:</span></span>
- <span data-ttu-id="13159-115">Créer un [mot de passe fort pour votre compte Github](https://github.com/settings/admin).</span><span class="sxs-lookup"><span data-stu-id="13159-115">Create a [strong password for your Github account](https://github.com/settings/admin).</span></span>
- <span data-ttu-id="13159-116">Activer [authentification à deux facteurs](https://github.com/settings/two_factor_authentication/configure).</span><span class="sxs-lookup"><span data-stu-id="13159-116">Enable [two-factor authentication](https://github.com/settings/two_factor_authentication/configure).</span></span>
- <span data-ttu-id="13159-117">Enregistrer votre [codes de récupération](https://github.com/settings/auth/recovery-codes) dans un endroit sûr.</span><span class="sxs-lookup"><span data-stu-id="13159-117">Save your [recovery codes](https://github.com/settings/auth/recovery-codes) in a safe place.</span></span>
- <span data-ttu-id="13159-118">Mise à jour votre [paramètres du profil public](https://github.com/settings/profile).</span><span class="sxs-lookup"><span data-stu-id="13159-118">Update your [public profile settings](https://github.com/settings/profile).</span></span>
   - <span data-ttu-id="13159-119">Définissez votre nom et envisagez de définir votre *messagerie Public* à *ne pas afficher mon adresse de messagerie*.</span><span class="sxs-lookup"><span data-stu-id="13159-119">Set your name, and consider setting your *Public email* to *Don't show my email address*.</span></span>
   - <span data-ttu-id="13159-120">Nous vous recommandons de vous chargez une image de profil, tel qu’une miniature apparaîtra sur les pages docs auxquelles vous contribuez.</span><span class="sxs-lookup"><span data-stu-id="13159-120">We recommend you upload a profile picture, as a thumbnail will be shown on docs pages to which you contribute.</span></span>
- <span data-ttu-id="13159-121">Si vous envisagez d’utiliser un flux de travail de ligne de commande, envisagez de configurer [Git Credential Manager pour Windows](https://github.com/Microsoft/Git-Credential-Manager-for-Windows/releases/latest) afin que vous n’êtes pas obligé d’entrer votre mot de passe chaque fois vous apportez une contribution.</span><span class="sxs-lookup"><span data-stu-id="13159-121">If you plan to use a command line workflow, consider setting up [Git Credential Manager for Windows](https://github.com/Microsoft/Git-Credential-Manager-for-Windows/releases/latest) so that you don't have to enter your password each time you make a contribution.</span></span>

<span data-ttu-id="13159-122">Suivi ces étapes est important, car le système de publication est lié à GitHub et vous allez être répertorié en tant qu’auteur ou contributeur pour chaque article à l’aide de votre alias de GitHub.</span><span class="sxs-lookup"><span data-stu-id="13159-122">Taking these steps is important, as the publishing system is tied to GitHub and you'll be listed as either author or contributor to each article using your GitHub alias.</span></span>

## <a name="editing-an-existing-article"></a><span data-ttu-id="13159-123">Modification d’un article existant</span><span class="sxs-lookup"><span data-stu-id="13159-123">Editing an existing article</span></span>

<span data-ttu-id="13159-124">Permet de mettre à jour le workflow suivant *un article existant* via GitHub dans un navigateur web :</span><span class="sxs-lookup"><span data-stu-id="13159-124">Use the following workflow to make updates to *an existing article* via GitHub in a web browser:</span></span>

1. <span data-ttu-id="13159-125">Accédez à l’article que vous souhaitez modifier dans le dossier « mixte en réalité-docs ».</span><span class="sxs-lookup"><span data-stu-id="13159-125">Navigate to the article you wish to edit in the "mixed-reality-docs" folder.</span></span>
2. <span data-ttu-id="13159-126">Dans le coin supérieur droit, sélectionnez le bouton Modifier (icône de crayon).</span><span class="sxs-lookup"><span data-stu-id="13159-126">Select the edit button (pencil icon) in the top right.</span></span> <span data-ttu-id="13159-127">Cela déviera automatiquement une branche JETABLE sur la branche « master ».</span><span class="sxs-lookup"><span data-stu-id="13159-127">This will automatically fork a disposable branch off the 'master' branch.</span></span>

   ![Modifier un article.](images/editpage.png)
3. <span data-ttu-id="13159-129">Modifier le contenu de l’article (voir [« Principes de base de Markdown »](#markdown-basics) ci-dessous pour obtenir des conseils).</span><span class="sxs-lookup"><span data-stu-id="13159-129">Edit the content of the article (see ["Markdown basics"](#markdown-basics) below for guidance).</span></span>
4. <span data-ttu-id="13159-130">Métadonnées de mise à jour comme il convient en haut de chaque article :</span><span class="sxs-lookup"><span data-stu-id="13159-130">Update metadata as relevant at the top of each article:</span></span>
   * <span data-ttu-id="13159-131">titre : Il s’agit du titre de la page qui s’affiche dans l’onglet du navigateur lors de l’affichage de l’article.</span><span class="sxs-lookup"><span data-stu-id="13159-131">title: This is the page title that appears in the browser tab when the article is being viewed.</span></span> <span data-ttu-id="13159-132">Comme il est utilisé pour les moteurs de recherche et l’indexation, vous ne devez pas modifier le titre, sauf si nécessaire (bien que cela soit moins critique avant de l’emplacement de la documentation publique).</span><span class="sxs-lookup"><span data-stu-id="13159-132">As this is used for SEO and indexing, you shouldn't change the title unless necessary (though this is less critical before documentation goes public).</span></span>
   * <span data-ttu-id="13159-133">Description : Écrire une brève description du contenu de l’article.</span><span class="sxs-lookup"><span data-stu-id="13159-133">description: Write a brief description of the article's content.</span></span> <span data-ttu-id="13159-134">Ceci simplifie les moteurs de recherche et de découverte.</span><span class="sxs-lookup"><span data-stu-id="13159-134">This aids in SEO and discovery.</span></span>
   * <span data-ttu-id="13159-135">Auteur : Si vous êtes le propriétaire principal de la page, ajoutez ici votre alias de GitHub.</span><span class="sxs-lookup"><span data-stu-id="13159-135">author: If you are the primary owner of the page, add your GitHub alias here.</span></span>
   * <span data-ttu-id="13159-136">ms.author: Si vous êtes le propriétaire principal de la page, ajoutez votre alias ici de Microsoft (vous n’avez pas besoin @microsoft.com, simplement l’alias).</span><span class="sxs-lookup"><span data-stu-id="13159-136">ms.author: If you are the primary owner of the page, add your Microsoft alias here (you don't need @microsoft.com, just the alias).</span></span>
   * <span data-ttu-id="13159-137">ms.date: Mettre à jour la date si vous êtes Ajout de contenu principale à la page, mais pas pour les correctifs de clarification, mise en forme, grammaire, ou d’orthographe.</span><span class="sxs-lookup"><span data-stu-id="13159-137">ms.date: Update the date if you're adding major content to the page, but not for fixes like clarification, formatting, grammar, or spelling.</span></span>
   * <span data-ttu-id="13159-138">mots clés : Mots clés aident à SEO (optimisation du moteur de recherche).</span><span class="sxs-lookup"><span data-stu-id="13159-138">keywords: Keywords aid in SEO (search engine optimization).</span></span> <span data-ttu-id="13159-139">Ajouter des mots clés, séparés par une virgule et un espace, qui sont spécifiques à votre article (mais sans aucune ponctuation après le dernier mot de clé dans votre liste) ; vous n’avez pas besoin ajouter des mots clés globales qui s’appliquent à tous les articles, comme ceux sont gérées ailleurs.</span><span class="sxs-lookup"><span data-stu-id="13159-139">Add keywords, separated by a comma and a space, that are specific to your article (but no punctuation after the last keyword in your list); you don't need to add global keywords that apply to all articles, as those are managed elsewhere.</span></span> 
5. <span data-ttu-id="13159-140">Lorsque vous avez terminé vos modifications de l’article, faites défiler et cliquez sur le **proposer un changement de fichier** bouton.</span><span class="sxs-lookup"><span data-stu-id="13159-140">When you've completed your article edits, scroll down and click the **Propose file change** button.</span></span>
6. <span data-ttu-id="13159-141">Dans la page suivante, cliquez sur **créer une demande de tirage** pour fusionner votre branche automatiquement créé dans « master ».</span><span class="sxs-lookup"><span data-stu-id="13159-141">On the next page, click **Create pull request** to merge your automatically-created branch into 'master.'</span></span>
7. <span data-ttu-id="13159-142">Répétez les étapes ci-dessus pour le prochain article que vous souhaitez modifier.</span><span class="sxs-lookup"><span data-stu-id="13159-142">Repeat the steps above for the next article you want to edit.</span></span>

## <a name="creating-a-new-article"></a><span data-ttu-id="13159-143">Créer un nouvel article</span><span class="sxs-lookup"><span data-stu-id="13159-143">Creating a new article</span></span>

<span data-ttu-id="13159-144">Utiliser le flux de travail suivant *créer de nouveaux articles* dans le référentiel de documentation via GitHub dans un navigateur web :</span><span class="sxs-lookup"><span data-stu-id="13159-144">Use the following workflow to *create new articles* in the documentation repo via GitHub in a web browser:</span></span>

1. <span data-ttu-id="13159-145">Créer une branche de la branche « master » MicrosoftDocs/réalité mixte (à l’aide de la **branchement** bouton dans le coin supérieur droit).</span><span class="sxs-lookup"><span data-stu-id="13159-145">Create a fork off the MicrosoftDocs/mixed-reality 'master' branch (using the **Fork** button in the top right).</span></span>

   ![Dupliquer (fork) de la branche principale.](images/forkbranch.png)
2. <span data-ttu-id="13159-147">Dans le dossier « mixte en réalité-docs », cliquez sur le **créer un nouveau fichier** bouton dans le coin supérieur droit.</span><span class="sxs-lookup"><span data-stu-id="13159-147">In the "mixed-reality-docs" folder, click the **Create new file** button in the top right.</span></span>
3. <span data-ttu-id="13159-148">Créer un nom de page pour l’article (utiliser des traits d’union plutôt que des espaces et n’utilisez pas signes de ponctuation ou des apostrophes) et ajouter « .md »</span><span class="sxs-lookup"><span data-stu-id="13159-148">Create a page name for the article (use hyphens instead of spaces and don't use punctuation or apostrophes) and append ".md"</span></span>

   ![Nommez votre nouvelle page.](images/newpagetitle.PNG)
   
   >[!IMPORTANT]
   ><span data-ttu-id="13159-150">Vérifiez que vous créez le nouvel article à partir du dossier « mixte en réalité-docs ».</span><span class="sxs-lookup"><span data-stu-id="13159-150">Make sure you create the new article from within the "mixed-reality-docs" folder.</span></span> <span data-ttu-id="13159-151">Vous pouvez le vérifier en recherchant « / docs de réalité mixte / » dans la nouvelle ligne de nom de fichier.</span><span class="sxs-lookup"><span data-stu-id="13159-151">You can confirm this by checking for "/mixed-reality-docs/" in the new file name line.</span></span>

4. <span data-ttu-id="13159-152">En haut de votre nouvelle page, ajoutez le bloc de métadonnées suivantes :</span><span class="sxs-lookup"><span data-stu-id="13159-152">At the top of your new page, add the following metadata block:</span></span>

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

5. <span data-ttu-id="13159-153">Renseignez les champs de métadonnées pertinentes par les instructions fournies dans le [section ci-dessus](#editing-an-existing-article).</span><span class="sxs-lookup"><span data-stu-id="13159-153">Fill in the relevant metadata fields per the instructions in the [section above](#editing-an-existing-article).</span></span>
6. <span data-ttu-id="13159-154">Écriture article contenu à l’aide [bases de Markdown](#markdown-basics).</span><span class="sxs-lookup"><span data-stu-id="13159-154">Write article content using [Markdown basics](#markdown-basics).</span></span>
7. <span data-ttu-id="13159-155">Ajouter un `## See also` section en bas de l’article avec des liens vers d’autres articles pertinents.</span><span class="sxs-lookup"><span data-stu-id="13159-155">Add a `## See also` section at the bottom of the article with links to other relevant articles.</span></span>
8. <span data-ttu-id="13159-156">Lorsque vous avez terminé, cliquez sur **validation nouveau fichier**.</span><span class="sxs-lookup"><span data-stu-id="13159-156">When finished, click **Commit new file**.</span></span>
9. <span data-ttu-id="13159-157">Cliquez sur **nouvelle requête de tirage** et fusionner la branche « master » de votre embranchement dans MicrosoftDocs/réalité mixte « master » (Assurez-vous que la flèche pointe la façon correcte).</span><span class="sxs-lookup"><span data-stu-id="13159-157">Click **New pull request** and merge your fork's 'master' branch into MicrosoftDocs/mixed-reality 'master' (make sure the arrow is pointing the correct way).</span></span>

   ![Créer la requête de tirage à partir de votre branchement dans MicrosoftDocs/réalité mixte](images/pr_to_master.PNG)

## <a name="markdown-basics"></a><span data-ttu-id="13159-159">Bases de markdown</span><span class="sxs-lookup"><span data-stu-id="13159-159">Markdown basics</span></span>

<span data-ttu-id="13159-160">Les ressources suivantes vous aideront à apprendre à modifier la documentation à l’aide de la langue de Markdown :</span><span class="sxs-lookup"><span data-stu-id="13159-160">The following resources will help you learn how to edit documentation using the Markdown language:</span></span>

- [<span data-ttu-id="13159-161">Bases de markdown</span><span class="sxs-lookup"><span data-stu-id="13159-161">Markdown basics</span></span>](https://help.github.com/articles/basic-writing-and-formatting-syntax/)
- [<span data-ttu-id="13159-162">Affiche de référence de markdown-at-a-glance</span><span class="sxs-lookup"><span data-stu-id="13159-162">Markdown-at-a-glance reference poster</span></span>](images/MarkdownPoster.pdf)
- [<span data-ttu-id="13159-163">Ressources supplémentaires pour l’écriture de Markdown pour docs.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="13159-163">Additional resources for writing Markdown for docs.microsoft.com</span></span>](https://docs.microsoft.com/contribute/how-to-write-use-markdown)

### <a name="adding-tables"></a><span data-ttu-id="13159-164">Ajout de tables</span><span class="sxs-lookup"><span data-stu-id="13159-164">Adding tables</span></span>

<span data-ttu-id="13159-165">En raison des tables de styles de docs.microsoft.com de façon, qu’elles n’auront bordures ou des styles personnalisés, même si vous essayez inline CSS.</span><span class="sxs-lookup"><span data-stu-id="13159-165">Because of the way docs.microsoft.com styles tables, they won’t have borders or custom styles, even if you try inline CSS.</span></span> <span data-ttu-id="13159-166">Il semblera fonctionner pendant une courte période de temps, mais finit par la plateforme supprimera le style hors de la table.</span><span class="sxs-lookup"><span data-stu-id="13159-166">It will appear to work for a short period of time, but eventually the platform will strip the styling out of the table.</span></span> <span data-ttu-id="13159-167">Par conséquent, planifiez et simplifier vos tables.</span><span class="sxs-lookup"><span data-stu-id="13159-167">So plan ahead and keep your tables simple.</span></span> <span data-ttu-id="13159-168">[Voici un site qui facilite les tableaux Markdown](http://www.tablesgenerator.com/markdown_tables).</span><span class="sxs-lookup"><span data-stu-id="13159-168">[Here’s a site that makes Markdown tables easy](http://www.tablesgenerator.com/markdown_tables).</span></span>

<span data-ttu-id="13159-169">Le [Docs Markdown Extension pour Visual Studio Code](https://docs.microsoft.com/teamblog/docs-extension) également rend table génération facile si vous utilisez [Visual Studio Code (voir ci-dessous)](#using-visual-studio-code) pour modifier la documentation.</span><span class="sxs-lookup"><span data-stu-id="13159-169">The [Docs Markdown Extension for Visual Studio Code](https://docs.microsoft.com/teamblog/docs-extension) also makes table generation easy if you're using [Visual Studio Code (see below)](#using-visual-studio-code) to edit the documentation.</span></span>

### <a name="adding-images"></a><span data-ttu-id="13159-170">Ajout d’images</span><span class="sxs-lookup"><span data-stu-id="13159-170">Adding images</span></span>

<span data-ttu-id="13159-171">Vous aurez besoin charger vos images dans le dossier « mixte en réalité-docs/images » dans le référentiel et puis les référencer en conséquence dans l’article.</span><span class="sxs-lookup"><span data-stu-id="13159-171">You’ll need to upload your images to the "mixed-reality-docs/images" folder in the repo, and then reference them appropriately in the article.</span></span> <span data-ttu-id="13159-172">Seront affiche automatiquement les images en taille réelle, ce qui signifie que si votre image est grande, il sera rempli toute la largeur de l’article.</span><span class="sxs-lookup"><span data-stu-id="13159-172">Images will automatically show up at full-size, which means if your image is large, it’ll fill the entire width of the article.</span></span> <span data-ttu-id="13159-173">Par conséquent, nous vous recommandons de dimensionnement préalable vos images avant de les télécharger.</span><span class="sxs-lookup"><span data-stu-id="13159-173">Thus, we recommend pre-sizing your images before uploading them.</span></span> <span data-ttu-id="13159-174">La largeur recommandée est comprise entre 600 et 700 pixels, bien que vous devez déterminer la taille vers le haut ou vers le bas si elle est une capture d’écran dense ou d’une fraction d’une capture d’écran, respectivement.</span><span class="sxs-lookup"><span data-stu-id="13159-174">The recommended width is between 600 and 700 pixels, though you should size up or down if it’s a dense screenshot or a fraction of a screenshot, respectively.</span></span>

>[!IMPORTANT]
><span data-ttu-id="13159-175">Vous pouvez uniquement charger des images à votre référentiel BIFURQUÉ avant la fusion.</span><span class="sxs-lookup"><span data-stu-id="13159-175">You can only upload images to your forked repo before merging.</span></span> <span data-ttu-id="13159-176">Par conséquent, si vous prévoyez d’ajouter des images à un article, vous devrez [utiliser Visual Studio Code](#using-visual-studio-code) d’abord ajouter les images au dossier « images » de votre embranchement ou vous assurer que vous avez effectué les éléments suivants dans un navigateur web :</span><span class="sxs-lookup"><span data-stu-id="13159-176">So, if you plan on adding images to an article, you'll need to [use Visual Studio Code](#using-visual-studio-code) to add the images to your fork's "images" folder first or make sure you've done the following in a web browser:</span></span>
>
>1. <span data-ttu-id="13159-177">Dupliqué le référentiel MicrosoftDocs/réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="13159-177">Forked the MicrosoftDocs/mixed-reality repo.</span></span>
>2. <span data-ttu-id="13159-178">Permet de modifier l’article dans votre fourche.</span><span class="sxs-lookup"><span data-stu-id="13159-178">Edited the article in your fork.</span></span>
>3. <span data-ttu-id="13159-179">Chargé les images que vous référencez dans votre article dans le dossier « mixte en réalité-docs/images » dans votre fourche.</span><span class="sxs-lookup"><span data-stu-id="13159-179">Uploaded the images you're referencing in your article to the "mixed-reality-docs/images" folder in your fork.</span></span>
>4. <span data-ttu-id="13159-180">Créé un **demande de tirage** pour fusionner votre branchement dans la branche « master » MicrosoftDocs/réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="13159-180">Created a **pull request** to merge your fork into the MicrosoftDocs/mixed-reality 'master' branch.</span></span>
>
><span data-ttu-id="13159-181">Pour savoir comment configurer votre propre référentiel BIFURQUÉ, suivez les instructions pour [créer un nouvel article](#creating-a-new-article).</span><span class="sxs-lookup"><span data-stu-id="13159-181">To learn how to set up your own forked repo, follow the instructions for [creating a new article](#creating-a-new-article).</span></span>

## <a name="previewing-your-work"></a><span data-ttu-id="13159-182">Afficher un aperçu de votre travail</span><span class="sxs-lookup"><span data-stu-id="13159-182">Previewing your work</span></span>

<span data-ttu-id="13159-183">Lors de la modification dans GitHub via un navigateur web, vous pouvez cliquer sur le **aperçu** onglet en haut de la page pour afficher un aperçu de votre travail avant de le valider.</span><span class="sxs-lookup"><span data-stu-id="13159-183">While editing in GitHub via a web browser, you can click the **Preview** tab near the top of the page to preview your work before committing.</span></span> 

>[!NOTE]
><span data-ttu-id="13159-184">Afficher un aperçu de vos modifications sur review.docs.microsoft.com est disponible uniquement pour les employés Microsoft</span><span class="sxs-lookup"><span data-stu-id="13159-184">Previewing your changes on review.docs.microsoft.com is only available to Microsoft employees</span></span>

<span data-ttu-id="13159-185">Les employés de Microsoft : une fois vos contributions ont été fusionnées dans la branche « master », vous pouvez voir l’aspect de la documentation avant d’entrer publique au https://review.docs.microsoft.com/windows/mixed-reality?branch=master (trouver votre article à l’aide de la table des matières dans la colonne de gauche).</span><span class="sxs-lookup"><span data-stu-id="13159-185">Microsoft employees: once your contributions have been merged into the 'master' branch, you can see what the documentation will look like before it goes public at https://review.docs.microsoft.com/windows/mixed-reality?branch=master (find your article using the table of contents in the left column).</span></span>

## <a name="editing-in-the-browser-vs-editing-with-a-desktop-client"></a><span data-ttu-id="13159-186">Modification dans le navigateur et de modification avec un client de bureau</span><span class="sxs-lookup"><span data-stu-id="13159-186">Editing in the browser vs. editing with a desktop client</span></span>

<span data-ttu-id="13159-187">Modification dans le navigateur le plus simple consiste à apporter des modifications rapides, toutefois, il existe quelques inconvénients :</span><span class="sxs-lookup"><span data-stu-id="13159-187">Editing in the browser is the easiest way to make quick changes, however, there are a few disadvantages:</span></span>

- <span data-ttu-id="13159-188">Vous n’obtenez pas vérifier l’orthographe.</span><span class="sxs-lookup"><span data-stu-id="13159-188">You don't get spell-check.</span></span>
- <span data-ttu-id="13159-189">Vous n’obtenez aucune liaison à puce à d’autres articles (vous devez taper manuellement le nom de fichier de l’article).</span><span class="sxs-lookup"><span data-stu-id="13159-189">You don't get any smart-linking to other articles (you have to manually type the article's filename).</span></span>
- <span data-ttu-id="13159-190">Il peut être une plaie pour charger et référencer les images.</span><span class="sxs-lookup"><span data-stu-id="13159-190">It can be a hassle to upload and reference images.</span></span>

<span data-ttu-id="13159-191">Si vous devez plutôt pas traiter ces problèmes, vous pouvez utiliser un client de bureau comme [Visual Studio Code](https://code.visualstudio.com/) avec quelques [des extensions utiles](#useful-extensions) pour contribuer à la documentation.</span><span class="sxs-lookup"><span data-stu-id="13159-191">If you'd rather not deal with these issues, you may prefer to use a desktop client like [Visual Studio Code](https://code.visualstudio.com/) with a couple [helpful extensions](#useful-extensions) to contribute to documentation.</span></span>

## <a name="using-visual-studio-code"></a><span data-ttu-id="13159-192">À l’aide de Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="13159-192">Using Visual Studio Code</span></span>

<span data-ttu-id="13159-193">Pour les raisons répertoriées [ci-dessus](#editing-in-the-browser-vs-editing-with-a-desktop-client), vous pouvez préférer à l’aide d’un client de bureau pour modifier la documentation au lieu d’un navigateur web.</span><span class="sxs-lookup"><span data-stu-id="13159-193">For the reasons listed [above](#editing-in-the-browser-vs-editing-with-a-desktop-client), you may prefer using a desktop client to edit documentation instead of a web browser.</span></span> <span data-ttu-id="13159-194">Nous vous recommandons d’utiliser [Visual Studio Code](https://code.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="13159-194">We recommend using [Visual Studio Code](https://code.visualstudio.com/).</span></span>

### <a name="setup"></a><span data-ttu-id="13159-195">Installation</span><span class="sxs-lookup"><span data-stu-id="13159-195">Setup</span></span>

<span data-ttu-id="13159-196">Suivez ces étapes pour configurer Visual Studio Code pour travailler avec ce référentiel :</span><span class="sxs-lookup"><span data-stu-id="13159-196">Follow these steps to configure Visual Studio Code to work with this repo:</span></span>

1. <span data-ttu-id="13159-197">Dans un navigateur web :</span><span class="sxs-lookup"><span data-stu-id="13159-197">In a web browser:</span></span>
    1. <span data-ttu-id="13159-198">Installer [Git pour votre PC](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="13159-198">Install [Git for your PC](https://git-scm.com/downloads).</span></span>
    2. <span data-ttu-id="13159-199">Installer [Visual Studio Code](https://code.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="13159-199">Install [Visual Studio Code](https://code.visualstudio.com/).</span></span>
    3. <span data-ttu-id="13159-200">[Dupliquer (fork) MicrosoftDocs/réalité mixte](#creating-a-new-article) si vous n’avez pas déjà.</span><span class="sxs-lookup"><span data-stu-id="13159-200">[Fork MicrosoftDocs/mixed-reality](#creating-a-new-article) if you haven't already.</span></span>
    4. <span data-ttu-id="13159-201">Dans votre fourche, cliquez sur **cloner ou télécharger** et copiez l’URL.</span><span class="sxs-lookup"><span data-stu-id="13159-201">In your fork, click **Clone or download** and copy the URL.</span></span>
2. <span data-ttu-id="13159-202">Créer un clone local de votre branchement dans Visual Studio Code :</span><span class="sxs-lookup"><span data-stu-id="13159-202">Create a local clone of your fork in Visual Studio Code:</span></span>
    1. <span data-ttu-id="13159-203">À partir de la **vue** menu, sélectionnez **Palette de commandes**.</span><span class="sxs-lookup"><span data-stu-id="13159-203">From the **View** menu, select **Command Palette**.</span></span>
    2. <span data-ttu-id="13159-204">Type « Git:Clone ».</span><span class="sxs-lookup"><span data-stu-id="13159-204">Type "Git:Clone."</span></span>
    3. <span data-ttu-id="13159-205">Collez l’URL que vous venez de copier.</span><span class="sxs-lookup"><span data-stu-id="13159-205">Paste the URL you just copied.</span></span>
    4. <span data-ttu-id="13159-206">Choisissez l’emplacement où enregistrer le clone sur votre PC.</span><span class="sxs-lookup"><span data-stu-id="13159-206">Choose where to save the clone on your PC.</span></span>
    5. <span data-ttu-id="13159-207">Cliquez sur **référentiel Open** dans la fenêtre contextuelle.</span><span class="sxs-lookup"><span data-stu-id="13159-207">Click **Open repo** in the pop-up.</span></span>

### <a name="editing-documentation"></a><span data-ttu-id="13159-208">Modification de documentation</span><span class="sxs-lookup"><span data-stu-id="13159-208">Editing documentation</span></span>

<span data-ttu-id="13159-209">Pour apporter des modifications à la documentation de Visual Studio Code, utilisez le workflow suivant :</span><span class="sxs-lookup"><span data-stu-id="13159-209">Use the following workflow to make changes to the documentation with Visual Studio Code:</span></span>

>[!NOTE]
><span data-ttu-id="13159-210">Tous les conseils pour [modification](#editing-an-existing-article) et [création](#creating-a-new-article) articles et le [principes fondamentaux de l’édition de Markdown](#markdown-basics), ci-dessus s’applique lors de l’utilisation de Visual Studio Code également.</span><span class="sxs-lookup"><span data-stu-id="13159-210">All the guidance for [editing](#editing-an-existing-article) and [creating](#creating-a-new-article) articles, and the [basics of editing Markdown](#markdown-basics), from above applies when using Visual Studio Code as well.</span></span>

1. <span data-ttu-id="13159-211">Assurez-vous que votre embranchement cloné est à jour avec le référentiel officiel.</span><span class="sxs-lookup"><span data-stu-id="13159-211">Make sure your cloned fork is up-to-date with the official repo.</span></span>
   1. <span data-ttu-id="13159-212">Dans un navigateur web, créez une demande de tirage pour synchroniser des modifications récentes apportées à partir d’autres contributeurs dans MicrosoftDocs/réalité mixte « master » à votre duplication (Assurez-vous que la flèche pointe la bonne façon).</span><span class="sxs-lookup"><span data-stu-id="13159-212">In a web browser, create a pull request to sync recent changes from other contributors in MicrosoftDocs/mixed-reality 'master' to your fork (make sure the arrow is pointing the right way).</span></span>
      
      ![Synchroniser les modifications MicrosoftDocs/réalité mixte pour votre duplication](images/sync_repos.PNG)
   2. <span data-ttu-id="13159-214">Dans Visual Studio Code, cliquez sur le bouton de synchronisation pour synchroniser votre embranchement fraîchement mis à jour sur le clone local.</span><span class="sxs-lookup"><span data-stu-id="13159-214">In Visual Studio Code, click the sync button to sync your freshly updated fork to the local clone.</span></span>
      
      ![Cliquez sur le bouton de synchronisation](images/sync_clone.png)
2. <span data-ttu-id="13159-216">Créez ou modifiez des articles dans votre dépôt cloné à l’aide de Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="13159-216">Create or edit articles in your cloned repo using Visual Studio Code.</span></span>
   1. <span data-ttu-id="13159-217">Modifier un ou plusieurs articles (ajouter des images à un dossier « images » si nécessaire).</span><span class="sxs-lookup"><span data-stu-id="13159-217">Edit one or more articles (add images to “images” folder if necessary).</span></span>
   2. <span data-ttu-id="13159-218">**Enregistrer** change dans **Explorer**.</span><span class="sxs-lookup"><span data-stu-id="13159-218">**Save** changes in **Explorer**.</span></span>
      
      ![Choisissez « Enregistrer toutes les » dans l’Explorateur](images/explorer_save.png)
   3. <span data-ttu-id="13159-220">**Valider tout** change dans **contrôle de code Source** (écrire le message de validation lorsque vous y êtes invité).</span><span class="sxs-lookup"><span data-stu-id="13159-220">**Commit all** changes in **Source Control** (write commit message when prompted).</span></span>
      
      ![Choisissez « Valider tout » dans le contrôle de code Source](images/source_control_commit.png)
   4. <span data-ttu-id="13159-222">Cliquez sur le **synchronisation** bouton pour synchroniser vos modifications sur origin (votre duplication sur GitHub).</span><span class="sxs-lookup"><span data-stu-id="13159-222">Click the **sync** button to sync your changes back to origin (your fork on GitHub).</span></span>
      
      ![Cliquez sur le bouton de synchronisation](images/sync_back.png)
3. <span data-ttu-id="13159-224">Dans un navigateur web, créez une demande de tirage pour synchroniser les nouvelles modifications de votre fourche vers MicrosoftDocs/réalité mixte « master » (Assurez-vous que la flèche pointe la façon correcte).</span><span class="sxs-lookup"><span data-stu-id="13159-224">In a web browser, create a pull request to sync new changes in your fork back to MicrosoftDocs/mixed-reality 'master' (make sure the arrow is pointing the correct way).</span></span>

   ![Créer la requête de tirage à partir de votre branchement dans MicrosoftDocs/réalité mixte](images/pr_to_master.PNG)

### <a name="useful-extensions"></a><span data-ttu-id="13159-226">Extensions utiles</span><span class="sxs-lookup"><span data-stu-id="13159-226">Useful extensions</span></span>

<span data-ttu-id="13159-227">Les extensions de Visual Studio Code suivantes sont très utiles lors de la documentation de modification :</span><span class="sxs-lookup"><span data-stu-id="13159-227">The following Visual Studio Code extensions are very useful when editing documentation:</span></span>

- <span data-ttu-id="13159-228">[Extension de Markdown docs pour Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=docsmsft.docs-authoring-pack) -utilisez **Alt + M** pour afficher un menu de docs authoring des options telles que :</span><span class="sxs-lookup"><span data-stu-id="13159-228">[Docs Markdown Extension for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=docsmsft.docs-authoring-pack) - Use **Alt+M** to bring up a menu of docs authoring options like:</span></span>
   - <span data-ttu-id="13159-229">Référence de recherche et des images que vous avez téléchargé.</span><span class="sxs-lookup"><span data-stu-id="13159-229">Search and reference images you've uploaded.</span></span>
   - <span data-ttu-id="13159-230">Ajouter mise en forme comme des listes, des tableaux et des légendes propres à docs comme `>[!NOTE]`.</span><span class="sxs-lookup"><span data-stu-id="13159-230">Add formatting like lists, tables, and docs-specific call-outs like `>[!NOTE]`.</span></span>
   - <span data-ttu-id="13159-231">Référence de recherche et des liens internes et les signets (liens vers des sections spécifiques au sein d’une page).</span><span class="sxs-lookup"><span data-stu-id="13159-231">Search and reference internal links and bookmarks (links to specific sections within a page).</span></span>
   - <span data-ttu-id="13159-232">Erreurs de mise en forme sont mis en surbrillance (pointez votre souris sur l’erreur pour en savoir plus).</span><span class="sxs-lookup"><span data-stu-id="13159-232">Formatting errors are highlighted (hover your mouse over the error to learn more).</span></span>
- <span data-ttu-id="13159-233">[Vérificateur orthographique de code](https://marketplace.visualstudio.com/items?itemName=streetsidesoftware.code-spell-checker) -mots mal orthographiés est soulignés ; avec le bouton droit sur un mot mal orthographié à le modifier ou l’enregistrer dans le dictionnaire.</span><span class="sxs-lookup"><span data-stu-id="13159-233">[Code Spell Checker](https://marketplace.visualstudio.com/items?itemName=streetsidesoftware.code-spell-checker) - misspelled words will be underlined; right-click on a misspelled word to change it or save it to the dictionary.</span></span>
