---
title: Comptes sur HoloLens
description: Comment configurer et gérer des comptes d’utilisateur sur HoloLens.
author: ''
ms.author: toddly
ms.date: 03/21/2018
ms.topic: article
keywords: HoloLens, utilisateur, compte, aad, adfs, compte microsoft, msa, informations d’identification
ms.openlocfilehash: 14f43b08b6ccb396bcf39c4082c840c65ac78cf9
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59594158"
---
# <a name="accounts-on-hololens"></a>Comptes sur HoloLens

Pendant l’installation de HoloLens initiale, les utilisateurs doivent se connecter avec le compte qu’ils souhaitent utiliser sur l’appareil. Ce compte peut être un compte Microsoft de consommateur ou un compte d’entreprise qui a été configuré dans Azure Active Directory (AAD) ou Active Directory Federation Services (ADFS).

Connexion à ce compte lors de l’installation crée un profil utilisateur sur l’appareil sur lequel l’utilisateur peut utiliser pour se connecter, et contre les toutes les applications doivent stocker leurs données. Ce même compte fournit également l’authentification unique pour les applications telles que Edge ou Skype via les API du Gestionnaire de compte Windows.

En outre, lorsque vous vous connectez à une entreprise ou d’un compte professionnel sur l’appareil, il peut-être également s’appliquer stratégie de gestion des appareils mobiles (MDM), si configuré par votre administrateur informatique.

Chaque fois que l’appareil redémarre ou sort de veille, les informations d’identification pour ce compte sont utilisées pour se connecter à nouveau. Si l’option appliquer une connexion à explicite est activée dans les paramètres, l’utilisateur devra saisir à nouveau leurs informations d’identification. Chaque fois que l’appareil redémarre après réception et en appliquant une mise à jour du système d’exploitation, un signe additionnel explicit est nécessaire.

## <a name="multi-user-support"></a>Prise en charge multi-utilisateur

>[!NOTE]
>Prise en charge multi-utilisateur nécessite Commercial Suite, comme il s’agit d’un [Windows Holographic for Business](https://docs.microsoft.com/hololens/hololens-upgrade-enterprise) fonctionnalité.

En commençant par le [mettre à jour du 10 avril 2018 Windows](release-notes-april-2018.md), HoloLens prend en charge plusieurs utilisateurs au sein du même client AAD. Pour l’utiliser, vous devez configurer l’appareil initialement avec un compte qui appartient à votre organisation. Par la suite, les autres utilisateurs à partir du même client sera en mesure de se connecter à l’appareil à partir de l’écran de connexion ou en appuyant sur la vignette de l’utilisateur sur le panneau de démarrage pour déconnecter l’utilisateur existant. 

Applications installées sur l’appareil sera disponibles pour tous les autres utilisateurs, mais chacune aura leurs propres données d’application et les préférences. Suppression d’une application supprimera également il pour tous les autres utilisateurs cependant. 

Vous pouvez supprimer les utilisateurs d’appareils à partir de l’appareil à récupérer de l’espace en cliquant sur Paramètres > comptes > autres personnes. Cela supprime également toutes les données d’application les autres utilisateurs à partir de l’appareil. 

## <a name="linked-accounts"></a>Comptes liés

Dans un compte d’appareil unique, les utilisateurs peuvent lier des informations d’identification du compte de serveur web supplémentaire pour les besoins de l’accès plus facile au sein des applications (par exemple, le Store) ou pour combiner l’accès aux ressources des données personnelles et professionnelles, similaires à la version bureau de Windows. Connexion à un compte supplémentaire de cette façon ne sépare pas les données utilisateur créées sur l’appareil, telles que des images ou les téléchargements. Une fois qu’un compte a été connecté à un appareil, les applications puissent effectuer utiliser avec votre autorisation pour réduire d’avoir à se connecter individuellement à chaque application.

## <a name="using-single-sign-on-within-an-app"></a>À l’aide de l’authentification unique au sein d’une application

En tant que développeur d’applications, vous pouvez tirer parti d’avoir une identité connecté sur HoloLens avec la [responsable de compte Windows API](https://msdn.microsoft.com/library/windows/apps/xaml/windows.security.authentication.web.core.aspx), tout comme vous le feriez sur d’autres appareils Windows. Des exemples de code de ces API sont disponibles [ici](http://go.microsoft.com/fwlink/p/?LinkId=620621).

Les interruptions de compte qui peuvent se produire telles que l’utilisateur demande de consentement pour les informations de compte, l’authentification à deux facteurs etc. doit être traitée lorsque l’application demande un jeton d’authentification.

Si votre application nécessite un type de compte spécifique n’a pas été lié précédemment, votre application peut demandons au système d’inviter l’utilisateur à ajouter un. Cette opération déclenche le volet de paramètres de compte à utiliser comme un enfant modal de votre application. Pour les applications 2D, cette fenêtre s’affiche directement via le centre de votre application et pour les applications Unity, cela prendra brièvement l’utilisateur de votre application HOLOGRAPHIQUE afin que cette fenêtre enfant peut être rendue. Personnalisation des commandes et des actions sur ce volet est décrite [ici](https://msdn.microsoft.com/library/windows/apps/windows.ui.applicationsettings.webaccountcommand.aspx).

## <a name="enterprise-and-other-authentication"></a>Enterprise et autres d’authentification

Si votre application effectue utiliser d’autres types d’authentification, tels que NTLM, Basic ou Kerberos, vous pouvez utiliser [l’interface utilisateur des informations d’identification Windows](https://msdn.microsoft.com/library/windows/apps/windows.security.credentials.ui.aspx) pour collecter, traiter et stocker des informations d’identification de l’utilisateur. L’expérience utilisateur pour la collecte de ces informations d’identification est très similaire à d’autres cloud piloté par les interruptions de compte et apparaissent sous la forme d’une application enfant sur votre application 2D ou brièvement suspendre une application Unity pour afficher l’interface utilisateur.

## <a name="deprecated-apis"></a>API déconseillées

Une différence pour le développement sur HoloLens de bureau est que [OnlineIDAuthenticator](https://msdn.microsoft.com/library/windows/apps/windows.security.authentication.onlineid.onlineidauthenticator.aspx) API n’est pas entièrement pris en charge. Bien qu’elle retournera qu'un jeton si le compte principal est en bonne autonome, interrompt tels que ceux décrits ci-dessus n’affichera pas d’interface utilisateur pour l’utilisateur et échouent à s’authentifier correctement le compte.

