---
title: Établissement d’une connexion sécurisée à l’aide de la communication à distance holographique
description: Cette page explique comment établir une connexion chiffrée sécurisée lors de l’utilisation de la communication à distance holographique.
author: bethau
ms.author: bethau
ms.date: 08/01/2019
ms.topic: article
keywords: HoloLens, communication à distance, communication à distance holographique
ms.openlocfilehash: 5bc039d7a1e500f577c4a30d2d082b718a45a8b4
ms.sourcegitcommit: ca949efe0279995a376750d89e23d7123eb44846
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68718073"
---
# <a name="establishing-a-secure-connection-with-holographic-remoting"></a>Établissement d’une connexion sécurisée à l’aide de la communication à distance holographique

>[!IMPORTANT]
>Ce guide est spécifique à la communication à distance holographique sur HoloLens 2.

Cette page explique comment établir une connexion chiffrée sécurisée lors de l’utilisation de la communication à distance holographique.

Lors de la diffusion en continu de contenu vers HoloLens 2 sur un réseau non sécurisé, tel qu’un WiFi ouvert ou Internet, il est fortement recommandé d’utiliser une connexion chiffrée.

>[!IMPORTANT]
>Même en cas d’utilisation d’un WiFi local approuvé à l’aide d’une connexion chiffrée, vous devez prendre en compte.

Pour pouvoir utiliser une connexion chiffrée, vous devez implémenter à la fois un [lecteur personnalisé](holographic-remoting-create-player.md) et une [application hôte personnalisée](holographic-remoting-create-host.md).

Le chiffrement est effectué à l’aide de l’implémentation TLS des plateformes sous-jacentes.

## <a name="basics-of-an-encrypted-connection"></a>Principes de base d’une connexion chiffrée

Les objets suivants doivent être implémentés pour permettre l’échange de certificats.

>[!TIP]
>L’implémentation d’interfaces WinRT peut facilement être C++effectuée à l’aide de/WinRT. Les [API Author avec C++/WinRT](https://docs.microsoft.com/en-us/windows/uwp/cpp-and-winrt-apis/author-apis) chapitre décrivent cela en détail.

>[!IMPORTANT]
>L' ```build\native\include\HolographicAppRemoting\Microsoft.Holographic.AppRemoting.idl``` intérieur du package NuGet contient une documentation détaillée sur l’API liée aux connexions sécurisées.

1) Objet de certificat, qui doit implémenter l' ```ICertificate``` interface.

    * Retourne le contenu binaire du certificat pfx à l’aide ```GetCertificatePfx``` de la méthode. Identique au contenu binaire d’un fichier. pfx.
    * Retourne le nom d’objet du ```GetSubjectName```certificat à l’aide de.
    * Retournez le mot de passe ```GetPfxPassword```pfx via. Retourne une chaîne vide pour un fichier PFX non protégé.

2) Fournisseur de certificats implémentant ```ICertificateProvider``` l’interface qui fournit un certificat lorsqu’il est ```GetCertificate``` demandé par le biais de la méthode.

3) Validateur de certificat implémentant l' ```ICertificateValidator``` interface. Sa tâche consiste à vérifier les certificats entrants.
    * La ```PerformSystemValidation``` méthode doit retourner ```true``` lorsque la plateforme sous-jacente doit valider la chaîne de ```false``` certificats entrants, sinon.
    * ```ValidateCertificate```est appelé par le contexte client pour demander la validation d’un certificat. Cette méthode accepte la chaîne de certificats (avec le premier certificat étant le sujet du certificat), le nom du serveur avec lequel la connexion est établie et si un contrôle de révocation doit être forcé. Le résultat de la validation du système sera fourni si la validation du système sous-jacent a été demandée. Pour continuer le traitement ```CertificateValidated``` avec le résultat approprié ou ```Cancel``` pour annuler la validation, vous devez appeler sur le ```ICertificateValidationCallback```passé.

En outre, pour permettre l’échange d’un jeton sécurisé, les objets suivants doivent être implémentés.

1) Fournisseur d’authentification qui implémente l' ```IAuthenticationProvider``` interface. Sa ```GetToken``` méthode est appelée par le contexte client pour demander un jeton pour l’authentification du client. Pour continuer ```TokenReceived``` à fournir le jeton d’authentification et poursuivre le processus de connexion ```Cancel``` , ou pour annuler le processus, il doit être appelé ```IAuthenticationProviderCallback```sur le passé.
2) Récepteur d’authentification qui implémente l' ```IAuthenticationReceiver``` interface. Sa tâche consiste à valider les jetons entrants.
    * La ```GetRealm``` méthode doit retourner le nom du domaine d’authentification.
    * La ```ValidateToken``` méthode est appelée par le contexte réseau du serveur pour demander la validation d’un jeton d’authentification client. Pour continuer, appelez ```ValidationCompleted``` pour signaler la fin de la validation ```Cancel``` ou pour rejeter la connexion cliente. La connexion cliente est acceptée ou rejetée en fonction du résultat de validation ```ValidationCompleted```passé à. 

Une fois ces objets implémentés ```ListenSecure``` , ils doivent être appelés à la place de ```Listen``` et ```ConnectSecure``` non ```Connect``` du contexte distant et du contexte de joueur, respectivement. ```ListenSecure```requiert un fournisseur de certificats et un récepteur d' ```Listen```authentification supplémentaires sur. ```ConnectSecure```requiert un fournisseur d’authentification supplémentaire et un validateur de certificat sur ```Connect```.

## <a name="see-also"></a>Voir aussi
* [Écriture d’une application hôte de communication à distance holographique](holographic-remoting-create-host.md)
* [Écriture d’une application de lecteur de communication à distance holographique personnalisée](holographic-remoting-create-player.md)
* [Résolution des problèmes et limitations de la communication à distance holographique](holographic-remoting-troubleshooting.md)
* [Termes du contrat de licence du logiciel de communication à distance holographique](https://docs.microsoft.com/en-us/legal/mixed-reality/microsoft-holographic-remoting-software-license-terms)
* [Déclaration de confidentialité Microsoft](https://go.microsoft.com/fwlink/?LinkId=521839)