---
title: Vue d’ensemble du développement JavaScript Mixed Reality
description: Vue d’ensemble du développement de réalité mixte à l’aide de JavaScript pour les casques immersifs Web, mobiles et Windows.
author: yonet
ms.author: ayyonet
ms.date: 04/10/2020
ms.topic: article
keywords: WebXR, WinMR, WebAR, WebVR, WindowsMixedReality, HoloLens, Windows Mixed Reality, Web VR, Web XR, Web Mr, Web AR, 360, 360 Video, 360 vidéos, 360 photo, 360 photos, 360 content, immersion Web, immersion-Web, IW, immersiveweb
ms.openlocfilehash: a1288e8f477f42b0937e797623fb83fe8f63685c
ms.sourcegitcommit: ba4c8c2a19bd6a9a181b2cec3cb8e0402f8cac62
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82835608"
---
# <a name="mixed-reality-development-with-javascript-overview"></a>Vue d’ensemble du développement de réalité mixte avec JavaScript

## <a name="mixed-reality-applications-on-the-web"></a>Applications de réalité mixte sur le Web

Les fonctionnalités de réalité mixte sont disponibles sur le Web à l’aide des [API d’appareil WebXR](https://developer.mozilla.org/en-US/docs/Web/API/WebXR_Device_API) et des [API WebVR déconseillées](webxr-overview.md). Pour les navigateurs qui ne prennent pas en charge les fonctionnalités WebXR complètes, vous pouvez ajouter des [polyremplissages WebXR](https://github.com/immersive-web/webxr-polyfill) à votre site Web.

## <a name="what-is-webxr-polyfill"></a>Qu’est-ce que le Polyfill WebXR

Une implémentation JavaScript de l’API d’appareil WebXR, ainsi que le module de manette WebXR. Ce Polyfill permet aux développeurs d’écrire sur la dernière spécification, en fournissant une prise en charge lorsqu’ils s’exécutent sur des navigateurs qui implémentent la spécification WebVR 1,1 ou sur des appareils mobiles sans prise en charge WebVR/WebXR.

## <a name="javascript-libraries-to-build-mixed-reality-applications-on-the-web"></a>Bibliothèques JavaScript pour créer des applications de réalité mixte sur le Web

## <a name="babylonjs"></a>Babylon. js

Babylon est un moteur 3D JavaScript qui facilite le développement de contenu 3D et d’applications immersifs. Avant de commencer à utiliser des applications immersifs, nous vous recommandons d’apprendre les principes fondamentaux du développement de Babylon. js.

Découvrez comment créer une application de réalité mixte avec Babylon dans la [section mise](https://doc.babylonjs.com/)en route. Jouez avec des exemples en 3D et leur code source à l’aide de la fonction de [terrain Babylon](https://doc.babylonjs.com/examples/). Plongez-vous dans le développement de la réalité mixte dans la [section WebXR](https://doc.babylonjs.com/how_to/introduction_to_webxr) de la documentation. 

## <a name="a-frame"></a>Frame-

Un frame est un framework JavaScript déclaratif qui permet de prendre en main la réalité virtuelle sur le Web. Pour en savoir plus, consultez la [documentation d’un cadre](https://aframe.io/) .

## <a name="threejs"></a>Trois. js

Trois. js est une bibliothèque 3D populaire pour créer des expériences immersifs. En savoir plus sur [trois. js](https://threejs.org/docs/index.html#manual/en/introduction/Creating-a-scene) dans la page de documentation et en explorant des [exemples](https://threejs.org/examples/#webgl_animation_cloth).

## <a name="webgl"></a>WebGL

Vous pouvez accéder aux API d’appareil WebXR directement à l’aide des API WebGL. WebGL (Web Graphics Library) est une API JavaScript pour le rendu de graphiques 3D et 2D interactifs à hautes performances dans n’importe quel navigateur Web compatible sans utiliser de plug-ins. en savoir plus sur les [API WebGL](https://developer.mozilla.org/en-US/docs/Web/API/WebGL_API).

## <a name="mixed-reality-native-mobile-applications-using-javascript"></a>Applications mobiles natives de réalité mixte utilisant JavaScript

Avec l’aide de quelques bibliothèques JavaScript, vous pouvez écrire vos expériences de réalité mixte une seule fois et les déployer sur des plateformes Web et natives telles que des casques Windows de réalité mixte, des appareils Android et iOS.

## <a name="babylon-native"></a>Babylon en mode natif

[Babylon Native](https://www.babylonjs.com/native/) Platform permet à quiconque de prendre son code Babylon. js et de créer une application native avec IT, ce qui déverrouille la puissance des technologies natives. Vous pouvez télécharger [Babylon native sur GitHub](https://github.com/BabylonJS/BabylonNative) et en savoir plus sur le [blog Babylon. js](https://medium.com/@babylonjs/babylon-native-821f1694fffc).

## <a name="react-native"></a>React Native

[REACT Native](https://reactnative.dev/) est une autre bibliothèque open source qui permet aux développeurs de créer à l’aide de JavaScript et de les déployer sur plusieurs plateformes. Vous pouvez télécharger [REACT native sur GitHub](https://github.com/facebook/react-native) et en savoir plus à ce sujet dans le [blog de REACT Native](https://reactnative.dev/blog/).

## <a name="see-also"></a> Voir aussi

* [Présentation de WebXR](webxr-overview.md)
* [Spécification de l’API d’appareil WebXR](https://immersive-web.github.io/webxr/)
* [Documentation de l’API d’appareil WebXR](https://developer.mozilla.org/en-US/docs/Web/API/WebXR_Device_API)
* [Immersiveweb. dev](https://immersiveweb.dev/)
* [Exemples WebXR](https://immersive-web.github.io/webxr-samples/)
* [Utilisation de Babylon. js pour créer des expériences WebXR](https://doc.babylonjs.com/how_to/introduction_to_webxr)
* [Windows Mixed Reality et le nouveau Microsoft Edge](https://docs.microsoft.com/windows/mixed-reality/new-microsoft-edge#introducing-the-new-microsoft-edge)
* [Github du W3C sur le Web immersif](https://github.com/immersive-web)
* [API WebGL](https://msdn.microsoft.com/library/bg182648(v=vs.85).aspx)
* [API du boîtier de manette](https://msdn.microsoft.com/library/dn743630(v=vs.85).aspx) et les [extensions de boîtier](https://w3c.github.io/gamepad/extensions.html)
* [Présentation de WebVR](webvr-overview.md)
