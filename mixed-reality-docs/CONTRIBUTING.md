---
title: Instructions de contribution
description: Comment contribuer à la documentation de Windows Mixed Reality.
author: mattwojo
ms.author: mattwoj
ms.date: 03/21/2018
ms.topic: article
ms.openlocfilehash: 934171f26571b3219bbe390aff44349fb6908f74
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73437128"
---
# <a name="contributing-to-windows-mixed-reality-developer-documentation"></a>Contribution à la documentation Windows Mixed Reality Developer

Bienvenue dans la [documentation du développeur référentiel pour Windows Mixed Reality](https://github.com/MicrosoftDocs/mixed-reality/tree/master/mixed-reality-docs). Tous les articles que vous créez ou modifiez dans ce référentiel **seront visibles par le public.** 

Les documents Windows Mixed Reality se trouvent désormais sur la plateforme docs.microsoft.com, qui utilise la démarque GitHub (avec les fonctionnalités Markdig). Fondamentalement, le contenu que vous modifiez dans ce référentiel est converti en pages mises en forme et stylisées qui s’affichent au https://docs.microsoft.com/windows/mixed-reality. 

Cette page présente les étapes et les instructions de base pour la contribution, ainsi que des liens vers les concepts de base de la marque. Merci pour votre contribution !

## <a name="before-you-start"></a>Avant de commencer

Si vous n’en avez pas déjà un, vous devez [créer un compte GitHub](https://github.com/join).

>[!NOTE]
>Si vous êtes un employé de Microsoft, liez votre compte GitHub à votre alias Microsoft sur le [portail Open source de Microsoft](https://repos.opensource.microsoft.com/). Rejoignez les organisations **« Microsoft »** et **« MicrosoftDocs »** ).

Lors de la configuration de votre compte GitHub, nous vous recommandons également les précautions de sécurité suivantes :
- Créez un [mot de passe fort pour votre compte GitHub](https://github.com/settings/admin).
- Activez [l’authentification à deux facteurs](https://github.com/settings/two_factor_authentication/configure).
- Enregistrez vos [codes de récupération](https://github.com/settings/auth/recovery-codes) dans un endroit sûr.
- Mettez à jour vos [paramètres de profil public](https://github.com/settings/profile).
   - Définissez votre nom et envisagez de configurer votre adresse de messagerie *publique* pour *ne pas afficher mon adresse de messagerie*.
   - Nous vous recommandons de télécharger une photo de profil, car une miniature s’affichera sur les pages docs auxquelles vous contribuez.
- Si vous envisagez d’utiliser un flux de travail de ligne de commande, pensez à configurer [git Credential Manager pour Windows](https://github.com/Microsoft/Git-Credential-Manager-for-Windows/releases/latest) afin de ne pas avoir à entrer votre mot de passe chaque fois que vous effectuez une contribution.

La réalisation de ces étapes est importante, car le système de publication est lié à GitHub et vous êtes mentionné comme auteur ou contributeur à chaque article à l’aide de votre alias GitHub.

## <a name="editing-an-existing-article"></a>Modification d’un article existant

Utilisez le flux de travail suivant pour effectuer des mises à jour d' *un article existant* via github dans un navigateur Web :

1. Accédez à l’article que vous souhaitez modifier dans le dossier « Mixed-Real-docs ».
2. Cliquez sur le bouton modifier (icône crayon) dans le coin supérieur droit. Cela permet de dupliquer automatiquement une branche jetable en dehors de la branche « master ».

   ![Modifier un article.](images/editpage.png)
3. Modifiez le contenu de l’article (consultez [« principes de base des démarques »](#markdown-basics) ci-dessous pour obtenir de l’aide).
4. Mettez à jour les métadonnées en haut de chaque article :
   * title : il s’agit du titre de la page qui s’affiche sous l’onglet navigateur lorsque l’article est affiché. Comme il est utilisé pour le SEO et l’indexation, vous ne devez pas modifier le titre sauf si cela est nécessaire (bien que cela soit moins critique avant que la documentation ne soit publique).
   * Description : rédigez une brève description du contenu de l’article. Cela facilite la découverte et le SEO.
   * Auteur : Si vous êtes le propriétaire principal de la page, ajoutez votre alias GitHub ici.
   * ms. Author : Si vous êtes le propriétaire principal de la page, ajoutez votre alias Microsoft ici (vous n’avez pas besoin de @microsoft.com, mais simplement de l’alias).
   * ms. Date : mettez à jour la date si vous ajoutez du contenu majeur à la page, mais pas pour des correctifs tels que la clarification, la mise en forme, la grammaire ou l’orthographe.
   * Mots clés : aide sur les mots clés dans SEO (optimisation du moteur de recherche). Ajoutez des mots clés, séparés par une virgule et un espace, qui sont spécifiques à votre article (mais aucune ponctuation après le dernier mot clé de votre liste). vous n’avez pas besoin d’ajouter des mots clés globaux qui s’appliquent à tous les articles, car ceux-ci sont gérés ailleurs. 
5. Une fois que vous avez terminé vos modifications, faites défiler la liste et cliquez sur le bouton **proposer un changement de fichier** .
6. Sur la page suivante, cliquez sur **créer une demande de tirage (pull Request** ) pour fusionner votre branche créée automatiquement dans « Master ».
7. Répétez les étapes ci-dessus pour le prochain article que vous souhaitez modifier.

## <a name="renaming-or-deleting-an-existing-article"></a>Attribution d’un nouveau nom ou suppression d’un article existant

Si votre modification renomme ou supprime un article existant, veillez à ajouter une redirection. De cette façon, toute personne disposant d’un lien vers l’article existant continuera de se retrouver au bon endroit. Les redirections sont gérées par le fichier. openpublishing. redirection. JSON à la racine du référentiel.

Pour ajouter une redirection à. openpublishing. redirection. JSON, ajoutez une entrée au tableau `redirections` :

```json
{
    "redirections": [
        {
            "source_path": "mixed-reality-docs/old-article.md",
            "redirect_url": "new-article#section-about-old-topic",
            "redirect_document_id": false
        },
```

- Le `source_path` est le chemin d’accès relatif au référentiel de l’ancien article que vous supprimez. Assurez-vous que le chemin d’accès commence par `mixed-reality-docs` et se termine par `.md`.
- Le `redirect_url` est l’URL publique relative de l’ancien article vers le nouvel article. Assurez-vous que cette URL **ne contient pas** de `mixed-reality-docs` ou de `.md`, car elle fait référence à l’URL publique et non au chemin d’accès au référentiel. La liaison à une section dans le nouvel article à l’aide de `#section` est autorisée. Vous pouvez également utiliser un chemin d’accès absolu à un autre site, si nécessaire.
- `redirect_document_id` indique si vous souhaitez conserver l’ID de document à partir du fichier précédent. La valeur par défaut est `false`. Utilisez `true` si vous souhaitez conserver la valeur d’attribut `ms.documentid` de l’article Redirigé. Si vous conservez l’ID de document, les données, telles que les affichages de page et les classements, seront transférées vers l’article cible. Procédez ainsi si la redirection est principalement un changement de nom, et non un pointeur vers un autre article qui couvre uniquement une partie du même contenu.

Si vous ajoutez une redirection, veillez à supprimer également l’ancien fichier.

## <a name="creating-a-new-article"></a>Création d’un article

Utilisez le flux de travail suivant pour *créer de nouveaux articles* dans la documentation référentiel via github dans un navigateur Web :

1. Créez une fourche à partir de la branche « master » MicrosoftDocs/de la réalité mixte (à l’aide du bouton de **branchement** dans le coin supérieur droit).

   ![Dupliquez la branche principale.](images/forkbranch.png)
2. Dans le dossier « Mixed-Real-docs », cliquez sur le bouton **créer un fichier** dans le coin supérieur droit.
3. Créer un nom de page pour l’article (utilisez des traits d’Union à la place d’espaces et n’utilisez pas de ponctuation ou d’apostrophes) et ajoutez « . MD »

   ![Nommez votre nouvelle page.](images/newpagetitle.PNG)
   
   >[!IMPORTANT]
   >Veillez à créer le nouvel article dans le dossier « Mixed-Real-docs ». Vous pouvez le vérifier en recherchant « /Mixed-Reality-docs/ » dans la ligne du nouveau nom de fichier.

4. En haut de votre nouvelle page, ajoutez le bloc de métadonnées suivant :

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

5. Renseignez les champs de métadonnées pertinents conformément aux instructions de la [section ci-dessus](#editing-an-existing-article).
6. Écrivez le contenu de l’article à l’aide des [principes fondamentaux](#markdown-basics).
7. Ajoutez une section `## See also` au bas de l’article avec des liens vers d’autres articles pertinents.
8. Lorsque vous avez terminé, cliquez sur **valider le nouveau fichier**.
9. Cliquez sur **nouvelle demande de tirage (pull Request** ) et fusionnez la branche’Master’de votre branche dans MicrosoftDocs/Mixed-Reality’Master' (Assurez-vous que la flèche pointe vers la bonne voie).

   ![Créer une requête de tirage (pull request) à partir de votre fourche dans MicrosoftDocs/Mixed-Reality](images/pr_to_master.PNG)

## <a name="markdown-basics"></a>Notions de base de la démarque

Les ressources suivantes vous permettront d’apprendre à modifier la documentation à l’aide du langage de démarque :

- [Notions de base de la démarque](https://help.github.com/articles/basic-writing-and-formatting-syntax/)
- [Affiche de référence de démarque-en un clin d’œil](images/MarkdownPoster.pdf)
- [Ressources supplémentaires pour l’écriture de la démarque pour docs.microsoft.com](https://docs.microsoft.com/contribute/how-to-write-use-markdown)

### <a name="adding-tables"></a>Ajout de tables

En raison de la façon dont les tableaux de styles docs.microsoft.com, ils n’ont pas de bordures ou de styles personnalisés, même si vous essayez le style CSS en ligne. Il semblera fonctionner pendant une période de temps limitée, mais la plateforme finira par supprimer le style de la table. Vous devez donc anticiper et garder vos tables simples. [Voici un site qui simplifie les tableaux de démarques](https://www.tablesgenerator.com/markdown_tables).

L' [extension docs de démarque pour Visual Studio code](https://docs.microsoft.com/teamblog/docs-extension) facilite également la génération de table si vous utilisez [Visual Studio code (voir ci-dessous)](#using-visual-studio-code) pour modifier la documentation.

### <a name="adding-images"></a>Ajouter des images

Vous devez charger vos images dans le dossier « Mixed-Real-docs/images » dans référentiel, puis les référencer de manière appropriée dans l’article. Les images s’affichent automatiquement à la taille maximale, ce qui signifie que si votre image est volumineuse, elle remplit toute la largeur de l’article. Par conséquent, nous vous recommandons de prédimensionner vos images avant de les charger. La largeur recommandée est comprise entre 600 et 700 pixels, même si vous devez monter ou diminuer la taille s’il s’agit d’une capture d’écran dense ou d’une fraction d’une capture d’écran, respectivement.

>[!IMPORTANT]
>Vous pouvez uniquement charger des images sur vos référentiel dupliqués avant la fusion. Par conséquent, si vous envisagez d’ajouter des images à un article, vous devez [utiliser Visual Studio code](#using-visual-studio-code) pour ajouter d’abord les images au dossier « images » de votre branche, ou vous assurer que vous avez effectué les opérations suivantes dans un navigateur Web :
>
>1. A fait la duplication du référentiel MicrosoftDocs/Mixed-Reality.
>2. Modification de l’article dans votre fourche.
>3. Téléchargez les images que vous référencez dans votre article dans le dossier « Mixed-Real-docs/images » de votre fourche.
>4. Création d’une **requête de tirage** pour fusionner votre fourche dans la branche « master » MicrosoftDocs/de la réalité mixte.
>
>Pour savoir comment configurer vos propres référentiel dupliqués, suivez les instructions de création d' [un nouvel article](#creating-a-new-article).

## <a name="previewing-your-work"></a>Aperçu de votre travail

Pendant la modification dans GitHub via un navigateur Web, vous pouvez cliquer sur l’onglet d' **Aperçu** en haut de la page pour afficher un aperçu de votre travail avant de le valider. 

>[!NOTE]
>L’aperçu de vos modifications sur review.docs.microsoft.com n’est disponible que pour les employés de Microsoft

Employés de Microsoft : une fois vos contributions fusionnées dans la branche principale, vous pouvez voir à quoi ressemblera la documentation avant qu’elle ne soit publique au https://review.docs.microsoft.com/windows/mixed-reality?branch=master (recherchez votre article à l’aide de la table des matières dans la colonne de gauche).

## <a name="editing-in-the-browser-vs-editing-with-a-desktop-client"></a>Modification dans le navigateur et modification avec un client Desktop

La modification dans le navigateur est le moyen le plus simple pour apporter des modifications rapides, toutefois, il existe quelques inconvénients :

- Vous n’avez pas de vérification orthographique.
- Vous n’avez pas de lien intelligent vers d’autres articles (vous devez taper manuellement le nom de fichier de l’article).
- Il peut être laborieux de charger et de référencer des images.

Si vous préférez ne pas traiter ces problèmes, vous préférerez peut-être utiliser un client de bureau comme [Visual Studio code](https://code.visualstudio.com/) avec quelques [Extensions utiles](#useful-extensions) pour contribuer à la documentation.

## <a name="using-visual-studio-code"></a>Utilisation de Visual Studio Code

Pour les raisons mentionnées [ci-dessus](#editing-in-the-browser-vs-editing-with-a-desktop-client), vous préférerez peut-être utiliser un client de bureau pour modifier la documentation au lieu d’un navigateur Web. Nous vous recommandons d’utiliser [Visual Studio code](https://code.visualstudio.com/).

### <a name="setup"></a>Installation

Procédez comme suit pour configurer Visual Studio Code pour qu’il fonctionne avec ce référentiel :

1. Dans un navigateur Web :
    1. Installez [git pour votre PC](https://git-scm.com/downloads).
    2. Installez [Visual Studio code](https://code.visualstudio.com/).
    3. [Duplication de MicrosoftDocs/Mixed-realisation](#creating-a-new-article) si vous ne l’avez pas déjà fait.
    4. Dans votre fourche, cliquez sur **cloner ou télécharger** et copiez l’URL.
2. Créez un clone local de votre fourche dans Visual Studio Code :
    1. Dans le menu **affichage** , sélectionnez **palette de commandes**.
    2. Tapez « git : Clone ».
    3. Collez l’URL que vous venez de copier.
    4. Choisissez l’emplacement où enregistrer le clone sur votre PC.
    5. Dans la fenêtre contextuelle, cliquez sur **ouvrir référentiel** .

### <a name="editing-documentation"></a>Modification de la documentation

Utilisez le flux de travail suivant pour apporter des modifications à la documentation avec Visual Studio Code :

>[!NOTE]
>Toutes les instructions relatives à la [modification](#editing-an-existing-article) et à la [création](#creating-a-new-article) d’articles, ainsi que les [principes fondamentaux de la modification de la démarque](#markdown-basics), ci-dessus s’appliquent également à l’utilisation de Visual Studio code.

1. Assurez-vous que votre fourche cloné est à jour avec la référentiel officielle.
   1. Dans un navigateur Web, créez une requête de tirage pour synchroniser les modifications récentes des autres contributeurs de MicrosoftDocs/Mixed-Reality’Master’sur votre fourche (Assurez-vous que la flèche pointe vers la bonne voie).
      
      ![Synchroniser les modifications de MicrosoftDocs/Mixed-Reality avec votre fourche](images/sync_repos.PNG)
   2. Dans Visual Studio Code, cliquez sur le bouton synchroniser pour synchroniser votre branche fraîchement mise à jour sur le clone local.
      
      ![Cliquez sur le bouton synchroniser.](images/sync_clone.png)
2. Créez ou modifiez des articles dans votre référentiel cloné à l’aide de Visual Studio Code.
   1. Modifiez un ou plusieurs articles (ajoutez des images au dossier « images » si nécessaire).
   2. **Enregistrer** les modifications dans l' **Explorateur**.
      
      ![Choisissez « Enregistrer tout » dans l’Explorateur](images/explorer_save.png)
   3. **Valide toutes les** modifications dans **le contrôle de code source** (message de validation en écriture quand vous y êtes invité).
      
      ![Choisissez « valider tout » dans le contrôle de code source](images/source_control_commit.png)
   4. Cliquez sur le bouton **synchroniser** pour resynchroniser vos modifications avec l’origine (votre fourche sur GitHub).
      
      ![Cliquez sur le bouton synchroniser.](images/sync_back.png)
3. Dans un navigateur Web, créez une requête de tirage pour synchroniser les modifications apportées à votre fourche en MicrosoftDocs/Mixed-Reality’Master' (Assurez-vous que la flèche pointe vers la bonne voie).

   ![Créer une requête de tirage (pull request) à partir de votre fourche dans MicrosoftDocs/Mixed-Reality](images/pr_to_master.PNG)

### <a name="useful-extensions"></a>Extensions utiles

Les extensions de Visual Studio Code suivantes sont très utiles lors de la modification de la documentation :

- [Extension docs de la marque pour Visual Studio code](https://marketplace.visualstudio.com/items?itemName=docsmsft.docs-authoring-pack) -utilisez **ALT + M** pour afficher un menu d’options de création de documents, comme :
   - Recherchez et référencez des images que vous avez téléchargées.
   - Ajoutez une mise en forme comme des listes, des tables et des appels spécifiques aux documents, comme `>[!NOTE]`.
   - Recherchez et référencez des liens et des signets internes (liens vers des sections spécifiques dans une page).
   - Les erreurs de mise en forme sont mises en surbrillance (pointez votre souris sur l’erreur pour en savoir plus).
- [Vérificateur orthographique de code](https://marketplace.visualstudio.com/items?itemName=streetsidesoftware.code-spell-checker) : les mots mal orthographiés sont soulignés. Cliquez avec le bouton droit sur un mot mal orthographié pour le modifier ou enregistrez-le dans le dictionnaire.
