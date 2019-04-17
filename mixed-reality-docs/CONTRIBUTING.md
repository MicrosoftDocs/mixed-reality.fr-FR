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
# <a name="contributing-to-windows-mixed-reality-developer-documentation"></a>Contribuez à la documentation de développement Windows Mixed Reality

Bienvenue dans le [référentiel public pour la documentation pour développeurs Windows Mixed Reality](https://github.com/MicrosoftDocs/mixed-reality/tree/master/mixed-reality-docs)! Des articles que vous créez ou modifiez dans ce dépôt **sera visible au public.** 

Documentation de Windows Mixed Reality se trouve désormais sur la plateforme docs.microsoft.com, qui utilise Markdown de GitHub-flavored (avec des fonctionnalités de Markdig). Essentiellement, le contenu que vous modifiez dans ce dépôt obtient transformé de pages mises en forme et stylisés qui s’affichent à https://docs.microsoft.com/windows/mixed-reality. 

Cette page décrit les étapes de base et les instructions pour votre contribution, ainsi que des liens vers les bases de Markdown. Nous vous remercions de votre contribution.

## <a name="before-you-start"></a>Avant de commencer

Si vous n’en avez déjà, vous devrez [créer un compte GitHub](https://github.com/join).

>[!NOTE]
>Si vous êtes un employé de Microsoft, liez votre compte GitHub à votre alias Microsoft sur le [portail de Microsoft Open Source](https://repos.opensource.microsoft.com/). Joindre le **« Microsoft »** et **« MicrosoftDocs »** organisations).

Lorsque vous configurez votre compte GitHub, nous vous recommandons également ces précautions de sécurité :
- Créer un [mot de passe fort pour votre compte Github](https://github.com/settings/admin).
- Activer [authentification à deux facteurs](https://github.com/settings/two_factor_authentication/configure).
- Enregistrer votre [codes de récupération](https://github.com/settings/auth/recovery-codes) dans un endroit sûr.
- Mise à jour votre [paramètres du profil public](https://github.com/settings/profile).
   - Définissez votre nom et envisagez de définir votre *messagerie Public* à *ne pas afficher mon adresse de messagerie*.
   - Nous vous recommandons de vous chargez une image de profil, tel qu’une miniature apparaîtra sur les pages docs auxquelles vous contribuez.
- Si vous envisagez d’utiliser un flux de travail de ligne de commande, envisagez de configurer [Git Credential Manager pour Windows](https://github.com/Microsoft/Git-Credential-Manager-for-Windows/releases/latest) afin que vous n’êtes pas obligé d’entrer votre mot de passe chaque fois vous apportez une contribution.

Suivi ces étapes est important, car le système de publication est lié à GitHub et vous allez être répertorié en tant qu’auteur ou contributeur pour chaque article à l’aide de votre alias de GitHub.

## <a name="editing-an-existing-article"></a>Modification d’un article existant

Permet de mettre à jour le workflow suivant *un article existant* via GitHub dans un navigateur web :

1. Accédez à l’article que vous souhaitez modifier dans le dossier « mixte en réalité-docs ».
2. Dans le coin supérieur droit, sélectionnez le bouton Modifier (icône de crayon). Cela déviera automatiquement une branche JETABLE sur la branche « master ».

   ![Modifier un article.](images/editpage.png)
3. Modifier le contenu de l’article (voir [« Principes de base de Markdown »](#markdown-basics) ci-dessous pour obtenir des conseils).
4. Métadonnées de mise à jour comme il convient en haut de chaque article :
   * titre : Il s’agit du titre de la page qui s’affiche dans l’onglet du navigateur lors de l’affichage de l’article. Comme il est utilisé pour les moteurs de recherche et l’indexation, vous ne devez pas modifier le titre, sauf si nécessaire (bien que cela soit moins critique avant de l’emplacement de la documentation publique).
   * Description : Écrire une brève description du contenu de l’article. Ceci simplifie les moteurs de recherche et de découverte.
   * Auteur : Si vous êtes le propriétaire principal de la page, ajoutez ici votre alias de GitHub.
   * ms.author: Si vous êtes le propriétaire principal de la page, ajoutez votre alias ici de Microsoft (vous n’avez pas besoin @microsoft.com, simplement l’alias).
   * ms.date: Mettre à jour la date si vous êtes Ajout de contenu principale à la page, mais pas pour les correctifs de clarification, mise en forme, grammaire, ou d’orthographe.
   * mots clés : Mots clés aident à SEO (optimisation du moteur de recherche). Ajouter des mots clés, séparés par une virgule et un espace, qui sont spécifiques à votre article (mais sans aucune ponctuation après le dernier mot de clé dans votre liste) ; vous n’avez pas besoin ajouter des mots clés globales qui s’appliquent à tous les articles, comme ceux sont gérées ailleurs. 
5. Lorsque vous avez terminé vos modifications de l’article, faites défiler et cliquez sur le **proposer un changement de fichier** bouton.
6. Dans la page suivante, cliquez sur **créer une demande de tirage** pour fusionner votre branche automatiquement créé dans « master ».
7. Répétez les étapes ci-dessus pour le prochain article que vous souhaitez modifier.

## <a name="creating-a-new-article"></a>Créer un nouvel article

Utiliser le flux de travail suivant *créer de nouveaux articles* dans le référentiel de documentation via GitHub dans un navigateur web :

1. Créer une branche de la branche « master » MicrosoftDocs/réalité mixte (à l’aide de la **branchement** bouton dans le coin supérieur droit).

   ![Dupliquer (fork) de la branche principale.](images/forkbranch.png)
2. Dans le dossier « mixte en réalité-docs », cliquez sur le **créer un nouveau fichier** bouton dans le coin supérieur droit.
3. Créer un nom de page pour l’article (utiliser des traits d’union plutôt que des espaces et n’utilisez pas signes de ponctuation ou des apostrophes) et ajouter « .md »

   ![Nommez votre nouvelle page.](images/newpagetitle.PNG)
   
   >[!IMPORTANT]
   >Vérifiez que vous créez le nouvel article à partir du dossier « mixte en réalité-docs ». Vous pouvez le vérifier en recherchant « / docs de réalité mixte / » dans la nouvelle ligne de nom de fichier.

4. En haut de votre nouvelle page, ajoutez le bloc de métadonnées suivantes :

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

5. Renseignez les champs de métadonnées pertinentes par les instructions fournies dans le [section ci-dessus](#editing-an-existing-article).
6. Écriture article contenu à l’aide [bases de Markdown](#markdown-basics).
7. Ajouter un `## See also` section en bas de l’article avec des liens vers d’autres articles pertinents.
8. Lorsque vous avez terminé, cliquez sur **validation nouveau fichier**.
9. Cliquez sur **nouvelle requête de tirage** et fusionner la branche « master » de votre embranchement dans MicrosoftDocs/réalité mixte « master » (Assurez-vous que la flèche pointe la façon correcte).

   ![Créer la requête de tirage à partir de votre branchement dans MicrosoftDocs/réalité mixte](images/pr_to_master.PNG)

## <a name="markdown-basics"></a>Bases de markdown

Les ressources suivantes vous aideront à apprendre à modifier la documentation à l’aide de la langue de Markdown :

- [Bases de markdown](https://help.github.com/articles/basic-writing-and-formatting-syntax/)
- [Affiche de référence de markdown-at-a-glance](images/MarkdownPoster.pdf)
- [Ressources supplémentaires pour l’écriture de Markdown pour docs.microsoft.com](https://docs.microsoft.com/contribute/how-to-write-use-markdown)

### <a name="adding-tables"></a>Ajout de tables

En raison des tables de styles de docs.microsoft.com de façon, qu’elles n’auront bordures ou des styles personnalisés, même si vous essayez inline CSS. Il semblera fonctionner pendant une courte période de temps, mais finit par la plateforme supprimera le style hors de la table. Par conséquent, planifiez et simplifier vos tables. [Voici un site qui facilite les tableaux Markdown](http://www.tablesgenerator.com/markdown_tables).

Le [Docs Markdown Extension pour Visual Studio Code](https://docs.microsoft.com/teamblog/docs-extension) également rend table génération facile si vous utilisez [Visual Studio Code (voir ci-dessous)](#using-visual-studio-code) pour modifier la documentation.

### <a name="adding-images"></a>Ajout d’images

Vous aurez besoin charger vos images dans le dossier « mixte en réalité-docs/images » dans le référentiel et puis les référencer en conséquence dans l’article. Seront affiche automatiquement les images en taille réelle, ce qui signifie que si votre image est grande, il sera rempli toute la largeur de l’article. Par conséquent, nous vous recommandons de dimensionnement préalable vos images avant de les télécharger. La largeur recommandée est comprise entre 600 et 700 pixels, bien que vous devez déterminer la taille vers le haut ou vers le bas si elle est une capture d’écran dense ou d’une fraction d’une capture d’écran, respectivement.

>[!IMPORTANT]
>Vous pouvez uniquement charger des images à votre référentiel BIFURQUÉ avant la fusion. Par conséquent, si vous prévoyez d’ajouter des images à un article, vous devrez [utiliser Visual Studio Code](#using-visual-studio-code) d’abord ajouter les images au dossier « images » de votre embranchement ou vous assurer que vous avez effectué les éléments suivants dans un navigateur web :
>
>1. Dupliqué le référentiel MicrosoftDocs/réalité mixte.
>2. Permet de modifier l’article dans votre fourche.
>3. Chargé les images que vous référencez dans votre article dans le dossier « mixte en réalité-docs/images » dans votre fourche.
>4. Créé un **demande de tirage** pour fusionner votre branchement dans la branche « master » MicrosoftDocs/réalité mixte.
>
>Pour savoir comment configurer votre propre référentiel BIFURQUÉ, suivez les instructions pour [créer un nouvel article](#creating-a-new-article).

## <a name="previewing-your-work"></a>Afficher un aperçu de votre travail

Lors de la modification dans GitHub via un navigateur web, vous pouvez cliquer sur le **aperçu** onglet en haut de la page pour afficher un aperçu de votre travail avant de le valider. 

>[!NOTE]
>Afficher un aperçu de vos modifications sur review.docs.microsoft.com est disponible uniquement pour les employés Microsoft

Les employés de Microsoft : une fois vos contributions ont été fusionnées dans la branche « master », vous pouvez voir l’aspect de la documentation avant d’entrer publique au https://review.docs.microsoft.com/windows/mixed-reality?branch=master (trouver votre article à l’aide de la table des matières dans la colonne de gauche).

## <a name="editing-in-the-browser-vs-editing-with-a-desktop-client"></a>Modification dans le navigateur et de modification avec un client de bureau

Modification dans le navigateur le plus simple consiste à apporter des modifications rapides, toutefois, il existe quelques inconvénients :

- Vous n’obtenez pas vérifier l’orthographe.
- Vous n’obtenez aucune liaison à puce à d’autres articles (vous devez taper manuellement le nom de fichier de l’article).
- Il peut être une plaie pour charger et référencer les images.

Si vous devez plutôt pas traiter ces problèmes, vous pouvez utiliser un client de bureau comme [Visual Studio Code](https://code.visualstudio.com/) avec quelques [des extensions utiles](#useful-extensions) pour contribuer à la documentation.

## <a name="using-visual-studio-code"></a>À l’aide de Visual Studio Code

Pour les raisons répertoriées [ci-dessus](#editing-in-the-browser-vs-editing-with-a-desktop-client), vous pouvez préférer à l’aide d’un client de bureau pour modifier la documentation au lieu d’un navigateur web. Nous vous recommandons d’utiliser [Visual Studio Code](https://code.visualstudio.com/).

### <a name="setup"></a>Installation

Suivez ces étapes pour configurer Visual Studio Code pour travailler avec ce référentiel :

1. Dans un navigateur web :
    1. Installer [Git pour votre PC](https://git-scm.com/downloads).
    2. Installer [Visual Studio Code](https://code.visualstudio.com/).
    3. [Dupliquer (fork) MicrosoftDocs/réalité mixte](#creating-a-new-article) si vous n’avez pas déjà.
    4. Dans votre fourche, cliquez sur **cloner ou télécharger** et copiez l’URL.
2. Créer un clone local de votre branchement dans Visual Studio Code :
    1. À partir de la **vue** menu, sélectionnez **Palette de commandes**.
    2. Type « Git:Clone ».
    3. Collez l’URL que vous venez de copier.
    4. Choisissez l’emplacement où enregistrer le clone sur votre PC.
    5. Cliquez sur **référentiel Open** dans la fenêtre contextuelle.

### <a name="editing-documentation"></a>Modification de documentation

Pour apporter des modifications à la documentation de Visual Studio Code, utilisez le workflow suivant :

>[!NOTE]
>Tous les conseils pour [modification](#editing-an-existing-article) et [création](#creating-a-new-article) articles et le [principes fondamentaux de l’édition de Markdown](#markdown-basics), ci-dessus s’applique lors de l’utilisation de Visual Studio Code également.

1. Assurez-vous que votre embranchement cloné est à jour avec le référentiel officiel.
   1. Dans un navigateur web, créez une demande de tirage pour synchroniser des modifications récentes apportées à partir d’autres contributeurs dans MicrosoftDocs/réalité mixte « master » à votre duplication (Assurez-vous que la flèche pointe la bonne façon).
      
      ![Synchroniser les modifications MicrosoftDocs/réalité mixte pour votre duplication](images/sync_repos.PNG)
   2. Dans Visual Studio Code, cliquez sur le bouton de synchronisation pour synchroniser votre embranchement fraîchement mis à jour sur le clone local.
      
      ![Cliquez sur le bouton de synchronisation](images/sync_clone.png)
2. Créez ou modifiez des articles dans votre dépôt cloné à l’aide de Visual Studio Code.
   1. Modifier un ou plusieurs articles (ajouter des images à un dossier « images » si nécessaire).
   2. **Enregistrer** change dans **Explorer**.
      
      ![Choisissez « Enregistrer toutes les » dans l’Explorateur](images/explorer_save.png)
   3. **Valider tout** change dans **contrôle de code Source** (écrire le message de validation lorsque vous y êtes invité).
      
      ![Choisissez « Valider tout » dans le contrôle de code Source](images/source_control_commit.png)
   4. Cliquez sur le **synchronisation** bouton pour synchroniser vos modifications sur origin (votre duplication sur GitHub).
      
      ![Cliquez sur le bouton de synchronisation](images/sync_back.png)
3. Dans un navigateur web, créez une demande de tirage pour synchroniser les nouvelles modifications de votre fourche vers MicrosoftDocs/réalité mixte « master » (Assurez-vous que la flèche pointe la façon correcte).

   ![Créer la requête de tirage à partir de votre branchement dans MicrosoftDocs/réalité mixte](images/pr_to_master.PNG)

### <a name="useful-extensions"></a>Extensions utiles

Les extensions de Visual Studio Code suivantes sont très utiles lors de la documentation de modification :

- [Extension de Markdown docs pour Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=docsmsft.docs-authoring-pack) -utilisez **Alt + M** pour afficher un menu de docs authoring des options telles que :
   - Référence de recherche et des images que vous avez téléchargé.
   - Ajouter mise en forme comme des listes, des tableaux et des légendes propres à docs comme `>[!NOTE]`.
   - Référence de recherche et des liens internes et les signets (liens vers des sections spécifiques au sein d’une page).
   - Erreurs de mise en forme sont mis en surbrillance (pointez votre souris sur l’erreur pour en savoir plus).
- [Vérificateur orthographique de code](https://marketplace.visualstudio.com/items?itemName=streetsidesoftware.code-spell-checker) -mots mal orthographiés est soulignés ; avec le bouton droit sur un mot mal orthographié à le modifier ou l’enregistrer dans le dictionnaire.
