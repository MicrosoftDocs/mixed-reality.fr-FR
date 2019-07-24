---
title: Entrée au clavier dans Unity
description: Unity fournit la classe TouchScreenKeyboard pour accepter l’entrée au clavier quand aucun clavier physique n’est disponible.
author: thetuvix
ms.author: alexturn
ms.date: 03/21/2018
ms.topic: article
keywords: clavier, entrée, Unity, touchscreenkeyboard
ms.openlocfilehash: 35f6f0df993931eea35db7b167110b341ea0c0f2
ms.sourcegitcommit: 915d3cc63a5571ba22ac4608589f3eca8da1bc81
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63515737"
---
# <a name="keyboard-input-in-unity"></a>Entrée au clavier dans Unity

**Espace de noms :** *UnityEngine*<br>
 **Type** : *[TouchScreenKeyboard](http://docs.unity3d.com/ScriptReference/TouchScreenKeyboard.html)*

Alors que HoloLens prend en charge de nombreuses formes d’entrée, y compris les claviers Bluetooth, la plupart des applications ne peuvent pas supposer que tous les utilisateurs disposent d’un clavier physique disponible. Si votre application nécessite une entrée de texte, une forme de clavier à l’écran doit être fournie.

Unity fournit la classe *[TouchScreenKeyboard](http://docs.unity3d.com/ScriptReference/TouchScreenKeyboard.html)* pour accepter l’entrée au clavier quand aucun clavier physique n’est disponible.

## <a name="hololens-system-keyboard-behavior-in-unity"></a>Comportement du clavier du système HoloLens dans Unity

Sur HoloLens, *TouchScreenKeyboard* utilise le clavier du système sur l’écran. Le clavier sur l’écran du système ne peut pas se superposer au-dessus d’une vue volumétrique. ainsi, Unity doit créer une vue XAML 2D secondaire pour afficher le clavier, puis revenir à la vue volumétrique une fois que l’entrée a été envoyée. Le workflow utilisateur se présente comme suit:
1. L’utilisateur effectue une action provoquant l’appel du code d’application *TouchScreenKeyboard*
    * L’application est responsable de la suspension de l’état de l’application avant d’appeler *TouchScreenKeyboard*
    * L’application peut se terminer avant de revenir à la vue volumétrique
2. Unity bascule vers une vue XAML 2D qui est placée automatiquement dans le monde
3. L’utilisateur entre du texte à l’aide du clavier du système et envoie ou annule
4. Le commutateur Unity revient à la vue volumétrique
    * L’application est responsable de la reprise de l’état de l’application lorsque le *TouchScreenKeyboard* est terminé
5. Le texte envoyé est disponible dans le *TouchScreenKeyboard*

### <a name="available-keyboard-views"></a>Affichages du clavier disponibles

Six différentes vues du clavier sont disponibles:
* Zone de texte sur une seule ligne
* Zone de texte sur une seule ligne avec titre
* Zone de texte multiligne
* Zone de texte multiligne avec titre
* Zone de mot de passe sur une seule ligne
* Zone de mot de passe sur une seule ligne avec titre

## <a name="how-to-enable-the-system-keyboard-in-unity"></a>Comment activer le clavier système dans Unity

Le clavier du système HoloLens est uniquement disponible pour les applications Unity qui sont exportées avec le «type de build UWP» défini sur «XAML». Vous effectuez des compromis lorsque vous choisissez «XAML» comme «type de build UWP» sur «D3D». Si vous n’êtes pas familiarisé avec ces compromis, vous souhaiterez peut-être explorer une [solution d’entrée alternative](#alternative-keyboard-options) au clavier du système.
1. Ouvrez le menu **fichier** et sélectionnez **paramètres de Build...**
2. Assurez-vous que la **plateforme** est définie sur **Windows Store**, que le **Kit de développement logiciel (SDK)** est défini sur **Universal 10**et que vous définissez le **type de build UWP** sur **XAML**.
3. Dans la boîte de dialogue **paramètres de build** , cliquez sur le bouton **paramètres du lecteur..** .
4. Sélectionner les **paramètres pour l’onglet Windows Store**
5. Développer le groupe **autres paramètres**
6. Dans la section **rendu** , activez la case à cocher **réalité virtuelle prise en charge** pour ajouter une nouvelle liste d' **appareils de réalité virtuelle**
7. S’assurer que **Windows holographique** apparaît dans la liste des kits de développement logiciel (SDK) de réalité virtuelle

>[!NOTE]
>Si vous ne Marquez pas la build comme une réalité virtuelle prise en charge avec l’appareil HoloLens, le projet sera exporté en tant qu’application XAML 2D.

## <a name="using-the-system-keyboard-in-your-unity-app"></a>Utilisation du clavier système dans votre application Unity

### <a name="declare-the-keyboard"></a>Déclarer le clavier

Dans la classe, déclarez une variable pour stocker le *TouchScreenKeyboard* et une variable qui contiendra la chaîne retournée par le clavier.

```cs
UnityEngine.TouchScreenKeyboard keyboard;
public static string keyboardText = "";
```

### <a name="invoke-the-keyboard"></a>Appeler le clavier

Lorsqu’un événement se produit en demandant une entrée au clavier, appelez l’une de ces fonctions en fonction du type d’entrée souhaité. Notez que le titre est spécifié dans le paramètre textPlaceholder.

```cs
// Single-line textbox
keyboard = TouchScreenKeyboard.Open("", TouchScreenKeyboardType.Default, false, false, false, false);

// Single-line textbox with title
keyboard = TouchScreenKeyboard.Open("", TouchScreenKeyboardType.Default, false, false, false, false, "Single-line title");

// Multi-line textbox
keyboard = TouchScreenKeyboard.Open("", TouchScreenKeyboardType.Default, false, true, false, false);

// Multi-line textbox with title
keyboard = TouchScreenKeyboard.Open("", TouchScreenKeyboardType.Default, false, true, false, false, "Multi-line Title");

// Single-line password box
keyboard = TouchScreenKeyboard.Open("", TouchScreenKeyboardType.Default, false, false, true, false);

// Single-line password box with title
keyboard = TouchScreenKeyboard.Open("", TouchScreenKeyboardType.Default, false, false, true, false, "Secure Single-line Title");
```

### <a name="retrieve-typed-contents"></a>Récupérer le contenu typé

Dans la boucle de mise à jour, vérifiez si le clavier a reçu une nouvelle entrée et stockez-la pour l’utiliser ailleurs.

```cs
if (TouchScreenKeyboard.visible == false && keyboard != null)
{
       if (keyboard.done == true)
       {
           keyboardText = keyboard.text;
           keyboard = null;
       }
}
```

## <a name="alternative-keyboard-options"></a>Autres options de clavier

Nous savons que le basculement d’une vue volumétrique dans une vue 2D n’est pas la méthode idéale pour obtenir une entrée de texte de l’utilisateur.

Les alternatives actuelles à l’utilisation du clavier système via Unity sont les suivantes:
* Utilisation de la dictée vocale pour l’entrée (<b>Remarque:</b> cela est souvent sujet à des erreurs pour les mots introuvables dans le dictionnaire et ne convient pas pour une entrée de mot de passe)
* Créer un clavier qui fonctionne en mode exclusif dans vos applications
