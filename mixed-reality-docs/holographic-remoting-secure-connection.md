---
title: Établissement d’une connexion sécurisée à l’aide de la communication à distance holographique
description: Cette page explique comment établir une connexion chiffrée sécurisée lors de l’utilisation de la communication à distance holographique.
author: FlorianBagarMicrosoft
ms.author: flbagar
ms.date: 03/11/2020
ms.topic: article
keywords: HoloLens, communication à distance, communication à distance holographique
ms.openlocfilehash: ac1170cb3e6d681fc164c3f4cee14da6ab6eb90b
ms.sourcegitcommit: 0a1af2224c9cbb34591b6cb01159b60b37dfff0c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/11/2020
ms.locfileid: "79092474"
---
# <a name="establishing-a-secure-connection-with-holographic-remoting"></a>Établissement d’une connexion sécurisée à l’aide de la communication à distance holographique

>[!IMPORTANT]
>Ce guide est spécifique à la communication à distance holographique sur HoloLens 2.

Cette page explique comment établir une connexion chiffrée sécurisée lors de l’utilisation de la communication à distance holographique.

Lors de la diffusion en continu de contenu vers HoloLens 2 sur un réseau non sécurisé, tel qu’un WiFi ouvert ou Internet, il est fortement recommandé d’utiliser une connexion chiffrée.

>[!IMPORTANT]
>Même en cas d’utilisation d’un WiFi local approuvé à l’aide d’une connexion chiffrée, vous devez prendre en compte.

Pour pouvoir utiliser une connexion chiffrée, vous devez implémenter à la fois un [lecteur personnalisé](holographic-remoting-create-player.md) et une [application distante personnalisée](holographic-remoting-create-host.md).

Le chiffrement est effectué à l’aide de l’implémentation TLS des plateformes sous-jacentes.

## <a name="basics-of-an-encrypted-connection"></a>Principes de base d’une connexion chiffrée

Les objets suivants doivent être implémentés pour permettre l’échange de certificats.

>[!TIP]
>L’implémentation d’interfaces WinRT peut facilement être C++effectuée à l’aide de/WinRT. Les [API Author avec C++/WinRT](https://docs.microsoft.com//windows/uwp/cpp-and-winrt-apis/author-apis) chapitre décrivent cela en détail.

>[!IMPORTANT]
>Le ```build\native\include\HolographicAppRemoting\Microsoft.Holographic.AppRemoting.idl``` à l’intérieur du package NuGet contient une documentation détaillée sur l’API liée aux connexions sécurisées.

1) Objet de certificat, qui doit implémenter l’interface ```ICertificate```.

    * Retourne le contenu binaire du certificat pfx à l’aide de la méthode ```GetCertificatePfx```. Identique au contenu binaire d’un fichier. pfx.
    * Retourne le nom d’objet du certificat à l’aide de ```GetSubjectName```.
    * Retourne le mot de passe pfx via ```GetPfxPassword```. Retourne une chaîne vide pour un fichier PFX non protégé.

2) Fournisseur de certificats implémentant l’interface ```ICertificateProvider``` qui fournit un certificat lorsqu’il est demandé par le biais de la méthode ```GetCertificate```.

3) Validateur de certificat implémentant l’interface ```ICertificateValidator```. Sa tâche consiste à vérifier les certificats entrants.
    * La méthode ```PerformSystemValidation``` doit retourner ```true``` lorsque la plateforme sous-jacente doit valider la chaîne de certificats entrants, ```false``` dans le cas contraire.
    * ```ValidateCertificate``` est appelée par le contexte client pour demander la validation d’un certificat. Cette méthode accepte la chaîne de certificats (avec le premier certificat étant le sujet du certificat), le nom du serveur avec lequel la connexion est établie et si un contrôle de révocation doit être forcé. Le résultat de la validation du système sera fourni si la validation du système sous-jacent a été demandée. Pour continuer le traitement des ```CertificateValidated``` avec le résultat approprié ou ```Cancel``` l’annulation de la validation doit être appelée sur le ```ICertificateValidationCallback```passé.

En outre, pour permettre l’échange d’un jeton sécurisé, les objets suivants doivent être implémentés.

1) Fournisseur d’authentification implémentant l’interface ```IAuthenticationProvider```. Sa méthode ```GetToken``` est appelée par le contexte client pour demander un jeton pour l’authentification du client. Pour continuer l' ```TokenReceived``` pour fournir le jeton d’authentification et poursuivre le processus de connexion ou ```Cancel``` pour annuler le processus doit être appelé sur le ```IAuthenticationProviderCallback```passé.
2) Récepteur d’authentification implémentant l’interface ```IAuthenticationReceiver```. Sa tâche consiste à valider les jetons entrants.
    * La méthode ```GetRealm``` doit retourner le nom du domaine d’authentification.
    * La méthode ```ValidateToken``` est appelée par le contexte réseau du serveur pour demander la validation d’un jeton d’authentification client. Pour continuer, appelez ```ValidationCompleted``` pour signaler la fin de la validation ou ```Cancel``` pour refuser la connexion cliente. La connexion cliente est acceptée ou rejetée en fonction du résultat de validation passé à ```ValidationCompleted```. 

Une fois ces objets implémentés ```ListenSecure``` doit être appelé au lieu de ```Listen``` et ```ConnectSecure``` au lieu de ```Connect``` respectivement dans le contexte distant et le contexte du joueur. ```ListenSecure``` requiert un fournisseur de certificats et un récepteur d’authentification supplémentaires sur ```Listen```. ```ConnectSecure``` requiert un fournisseur d’authentification supplémentaire et un validateur de certificat sur ```Connect```.

## <a name="see-also"></a>Voir aussi
* [Écriture d’une application distante de communication à distance holographique](holographic-remoting-create-host.md)
* [Écriture d’une application de lecteur de communication à distance holographique personnalisée](holographic-remoting-create-player.md)
* [Résolution des problèmes et limitations de la communication à distance holographique](holographic-remoting-troubleshooting.md)
* [Termes du contrat de licence de la communication à distance holographique](https://docs.microsoft.com//legal/mixed-reality/microsoft-holographic-remoting-software-license-terms)
* [Déclaration de confidentialité Microsoft](https://go.microsoft.com/fwlink/?LinkId=521839)
