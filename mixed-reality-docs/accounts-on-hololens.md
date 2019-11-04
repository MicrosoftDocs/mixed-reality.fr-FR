---
title: Comptes sur HoloLens
description: Comment configurer et gérer des comptes d’utilisateur sur HoloLens.
author: tmlyon
ms.author: toddly
ms.date: 03/21/2018
ms.topic: article
keywords: HoloLens, utilisateur, compte, AAD, ADFS, compte Microsoft, MSA, informations d’identification
ms.openlocfilehash: 5579cf53948b8bdbd4b41973dde7b8fc70a5aa31
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73437084"
---
# <a name="accounts-on-hololens"></a>Comptes sur HoloLens

Lors de la configuration de HoloLens initiale, les utilisateurs doivent se connecter avec le compte qu’ils souhaitent utiliser sur l’appareil. Ce compte peut être un client compte Microsoft ou un compte d’entreprise configuré dans Azure Active Directory (AAD) ou Services ADFS (ADFS).

La connexion à ce compte pendant l’installation crée un profil utilisateur sur l’appareil que l’utilisateur peut utiliser pour se connecter, et pour lequel toutes les applications stockent leurs données. Ce même compte fournit également une authentification unique pour les applications telles que Edge ou Skype via les API du gestionnaire de comptes Windows.

En outre, lorsque vous vous connectez à un compte d’entreprise ou d’entreprise sur l’appareil, il peut également appliquer la stratégie de gestion des appareils mobiles (MDM), si elle est configurée par votre administrateur informatique.

Chaque fois que le périphérique redémarre ou reprend à partir de la veille, les informations d’identification de ce compte sont utilisées pour se connecter à nouveau. Si l’option permettant d’appliquer une connexion explicite est activée dans les paramètres, l’utilisateur sera obligé de taper à nouveau ses informations d’identification. Chaque fois que l’appareil redémarre après la réception et l’application d’une mise à jour du système d’exploitation, une connexion explicite est requise.

## <a name="multi-user-support"></a>Prise en charge multi-utilisateur

>[!NOTE]
>La prise en charge de plusieurs utilisateurs requiert la suite commerciale, car il s’agit d’une fonctionnalité [Windows holographique for Business](https://docs.microsoft.com/hololens/hololens-upgrade-enterprise) .

À compter de la [mise à jour 2018 de Windows 10 avril](release-notes-april-2018.md), HoloLens prend en charge plusieurs utilisateurs au sein du même locataire AAD. Pour ce faire, vous devez d’abord configurer l’appareil à l’aide d’un compte qui appartient à votre organisation. Par la suite, les autres utilisateurs du même locataire pourront se connecter à l’appareil à partir de l’écran de connexion ou en appuyant sur la vignette de l’utilisateur dans le panneau Démarrer pour déconnecter l’utilisateur existant. 

Les applications installées sur l’appareil seront disponibles pour tous les autres utilisateurs, mais chacune aura leurs propres données et préférences d’application. Si vous supprimez une application, elle est également supprimée pour tous les autres utilisateurs. 

Vous pouvez supprimer des utilisateurs d’appareils de l’appareil pour récupérer de l’espace en accédant à paramètres > comptes > autres personnes. Cette opération supprime également toutes les données d’application des autres utilisateurs de l’appareil. 

## <a name="linked-accounts"></a>Comptes liés

Dans un compte d’appareil unique, les utilisateurs peuvent lier des informations d’identification de compte Web supplémentaires pour faciliter l’accès au sein des applications (par exemple, le Store) ou associer l’accès à des ressources personnelles et professionnelles, comme la version de bureau de Windows. La connexion à un compte supplémentaire de cette manière ne sépare pas les données utilisateur créées sur l’appareil, telles que les images ou les téléchargements. Une fois qu’un compte a été connecté à un appareil, les applications peuvent l’utiliser avec votre autorisation afin de réduire la connexion individuelle à chaque application.

## <a name="using-single-sign-on-within-an-app"></a>Utilisation de l’authentification unique dans une application

En tant que développeur d’applications, vous pouvez tirer parti d’une identité connectée à HoloLens avec les [API du gestionnaire de compte Windows](https://msdn.microsoft.com/library/windows/apps/xaml/windows.security.authentication.web.core.aspx), comme vous le feriez sur d’autres appareils Windows. Des exemples de code pour ces API sont disponibles [ici](https://go.microsoft.com/fwlink/p/?LinkId=620621).

Les interruptions de compte qui peuvent se produire, telles que la demande de consentement de l’utilisateur pour les informations de compte, l’authentification à deux facteurs, etc., doivent être gérées lorsque l’application demande un jeton d’authentification.

Si votre application nécessite un type de compte spécifique qui n’a pas été lié précédemment, votre application peut demander au système d’inviter l’utilisateur à en ajouter une. Le volet Paramètres du compte sera alors lancé comme un enfant modal de votre application. Pour les applications 2D, cette fenêtre est restituée directement au centre de votre application et pour les applications Unity, l’utilisateur est extrait brièvement de votre application holographique afin que cette fenêtre enfant puisse être rendue. La personnalisation des commandes et des actions sur ce volet est décrite [ici](https://msdn.microsoft.com/library/windows/apps/windows.ui.applicationsettings.webaccountcommand.aspx).

## <a name="enterprise-and-other-authentication"></a>Authentification d’entreprise et autres

Si votre application utilise d’autres types d’authentification, tels que NTLM, de base ou Kerberos, vous pouvez utiliser l' [interface utilisateur des informations d’identification Windows](https://msdn.microsoft.com/library/windows/apps/windows.security.credentials.ui.aspx) pour collecter, traiter et stocker les informations d’identification de l’utilisateur. L’expérience utilisateur pour la collecte de ces informations d’identification est très similaire à celle d’autres interruptions de compte pilotées par le Cloud. elle apparaîtra en tant qu’application enfant sur votre application 2D ou suspendra brièvement une application Unity pour afficher l’interface utilisateur.

## <a name="deprecated-apis"></a>API déconseillées

L’une des différences de développement sur HoloLens à partir du Bureau est que l’API [OnlineIDAuthenticator](https://msdn.microsoft.com/library/windows/apps/windows.security.authentication.onlineid.onlineidauthenticator.aspx) n’est pas entièrement prise en charge. Bien qu’elle retourne un jeton si le compte principal est en bonne position, les interruptions telles que celles décrites ci-dessus n’affichent pas d’interface utilisateur pour l’utilisateur et ne parviennent pas à authentifier correctement le compte.

