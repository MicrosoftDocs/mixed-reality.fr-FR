---
title: Entrée au clavier dans Unity
description: Unity fournit la classe TouchScreenKeyboard pour accepter une entrée de clavier lorsqu’il n’existe pas de clavier physique disponible.
author: thetuvix
ms.author: alexturn
ms.date: 03/21/2018
ms.topic: article
keywords: unity d’entrée, clavier, touchscreenkeyboard
ms.openlocfilehash: 35f6f0df993931eea35db7b167110b341ea0c0f2
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59597040"
---
# <a name="keyboard-input-in-unity"></a>Entrée au clavier dans Unity

**Namespace :** *UnityEngine*<br>
 **Type** : *[TouchScreenKeyboard](http://docs.unity3d.com/ScriptReference/TouchScreenKeyboard.html)*

HoloLens prend en charge de nombreux formulaires d’entrée, y compris les claviers, la plupart des applications ne peut pas supposer que tous les utilisateurs auront un clavier physique disponible. Si votre application nécessite la saisie de texte, une forme de clavier de l’écran doit être fournie.

Unity fournit le *[TouchScreenKeyboard](http://docs.unity3d.com/ScriptReference/TouchScreenKeyboard.html)* classe permettant d’accepter l’entrée au clavier lorsqu’il n’existe pas de clavier physique disponible.

## <a name="hololens-system-keyboard-behavior-in-unity"></a>Comportement du clavier système HoloLens dans Unity

Sur HoloLens, le *TouchScreenKeyboard* se sert du système sur le clavier de l’écran. Le système sur le clavier visuel est incapable de superposer sur une vue volumétrique Unity doit donc créer une vue XAML 2D secondaire pour afficher le clavier puis à revenir dans la vue volumétrique une fois que l’entrée a été envoyée. Le flux de l’utilisateur se déroule comme suit :
1. L’utilisateur effectue une action à l’origine du code d’application pour appeler *TouchScreenKeyboard*
    * L’application est responsable de l’état de mise en pause l’application avant d’appeler *TouchScreenKeyboard*
    * L’application peut se fermer avant de basculer jamais revenir à la vue volumétrique
2. Unity bascule vers une vue XAML 2D qui est placés automatiquement dans le monde
3. L’utilisateur entre du texte à l’aide du clavier système et soumet ou annule
4. Unity bascule vers la vue volumétrique
    * L’application est responsable de l’application de reprise état lorsque le *TouchScreenKeyboard* est effectuée
5. Texte soumis est disponible dans le *TouchScreenKeyboard*

### <a name="available-keyboard-views"></a>Vues de clavier disponibles

Il existe six clavier différentes vues disponibles :
* Zone de texte monoligne
* Zone de texte monoligne avec titre
* Zone de texte multiligne
* Zone de texte multiligne avec titre
* Zone de mot de passe une ligne
* Zone de mot de passe une ligne avec titre

## <a name="how-to-enable-the-system-keyboard-in-unity"></a>Comment activer le clavier système dans Unity

Le clavier système HoloLens est uniquement disponible pour les applications Unity qui sont exportées avec le « UWP Build Type » défini sur « XAML ». Il existe des compromis que vous effectuez lorsque vous choisissez « XAML » comme le « Type de Build UWP » sur « D3D ». Si vous n’êtes pas familiarisé avec ces compromis, vous pouvez Explorer une [solution d’entrée de remplacement](#alternative-keyboard-options) au clavier système.
1. Ouvrez le **fichier** menu et sélectionnez **paramètres de Build...**
2. Garantir la **plateforme** a la valeur **Windows Store**, le **SDK** a la valeur **universelle 10**et définissez la **Type de Build UWP**  à **XAML**.
3. Dans le **paramètres de Build** boîte de dialogue, cliquez sur le **paramètres du lecteur...**  bouton
4. Sélectionnez le **paramètres pour Windows Store** onglet
5. Développez le **autres paramètres** groupe
6. Dans le **rendu** section, vérifiez le **virtuel pris en charge de réalité** case à cocher pour ajouter un nouveau **des appareils de réalité virtuelle** liste
7. Vérifiez **Windows HOLOGRAPHIQUE** s’affiche dans la liste des kits SDK de réalité virtuelle

>[!NOTE]
>Si vous ne marquez pas la build en tant que la prise en charge du réalité virtuelle avec l’appareil HoloLens, le projet sera exporter en tant qu’une application XAML 2D.

## <a name="using-the-system-keyboard-in-your-unity-app"></a>À l’aide du clavier système dans votre application Unity

### <a name="declare-the-keyboard"></a>Déclarez le clavier

Dans la classe, déclarez une variable pour stocker le *TouchScreenKeyboard* et retourne une variable pour contenir la chaîne à l’aide du clavier.

```cs
UnityEngine.TouchScreenKeyboard keyboard;
public static string keyboardText = "";
```

### <a name="invoke-the-keyboard"></a>Appeler le clavier

Lorsqu’un événement survient demandeur entrée au clavier, appelez une de ces fonctions selon le type d’entrée que vous le souhaitez. Notez que le titre est spécifié dans le paramètre textPlaceholder.

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

Dans la boucle de mise à jour, vérifiez si le clavier a reçu une nouvelle entrée et stockez-le pour une utilisation ultérieure.

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

## <a name="alternative-keyboard-options"></a>Options de remplacement de clavier

Nous sommes conscients que hors d’une vue volumétrique dans une vue en 2D de commutation n’est pas le moyen idéal pour obtenir une entrée de texte à partir de l’utilisateur.

Les alternatives actuels pour exploiter le clavier système via Unity incluent :
* À l’aide de la dictée vocale pour l’entrée (<b>Remarque :</b> cela est souvent sujette aux erreurs dans introuvable dans le dictionnaire de mots et ne convient pas pour l’entrée de mot de passe)
* Créer un clavier fonctionne dans votre vue exclusif des applications
