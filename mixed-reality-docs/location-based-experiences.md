---
title: Divertissement basé sur l’emplacement avec Windows Mixed Reality
description: Accédez aux objets natifs holographiques sous-jacents dans Unity.
author: jessemcculloch
ms.author: ishitak
ms.date: 08/22/2019
ms.topic: article
keywords: réalité mixte, VR, LBE, location
ms.openlocfilehash: e23d17ff2b07c636c98a9f19a5dd20f4dc558bf7
ms.sourcegitcommit: 5d3be2d7569d912011ea114c0a283bc3c635d5df
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69983397"
---
# <a name="location-based-entertainment-with-windows-mixed-reality"></a>Divertissement basé sur l’emplacement avec Windows Mixed Reality

Au cours des dernières années, nous avons observé un incroyable volume de croissance et d’innovation dans la catégorie de divertissements basée sur l’emplacement. Les systèmes traditionnels tels que les parcs de thèmes et les théâtres ont commencé à offrir des expériences immersifs à plusieurs joueurs comme des expériences complémentaires pour les emplacements et les installations existantes. Les nouveaux opérateurs et emplacements permettent de créer des expériences multilecteurs et multi-joueurs uniques à un prix intéressant aux masses. Toutes ces expériences poussent l’enveloppe pour ce qui est possible avec la réalité mixte.

Ce document est un guide de prise en main de Windows Mixed Reality dans la catégorie divertissements basée sur l’emplacement. Les instructions ci-dessous peuvent également s’appliquer à des expériences basées sur l’emplacement au-delà des loisirs, telles que la formation, la conception de produits ou d’autres cas d’usage.

## <a name="engineering-faq"></a>FAQ sur l’ingénierie

### <a name="hardware"></a>Matériel

**Q : Quel matériel est disponible auprès de Microsoft et de ses partenaires que je peux utiliser dans mon programme d’installation?**

R : Microsoft et ses partenaires OEM proposent un portefeuille attrayant d’appareils en fonction de vos besoins.  

Si les expériences que vous fournissez à vos clients requièrent des casques de réalité virtuelle, les casques sur le marché suivants de HP, Samsung et Acer sont très adaptés. Chaque casque possède ses propres attributs différenciés. Pour plus d’informations, reportez-vous à la suite.

Réverbération HP: [Détails](https://hp.com/go/Reverbpro)

Samsung Odyssey +: [Détails](https://www.samsung.com/us/computing/hmd/windows-mixed-reality/hmd-odyssey-windows-mixed-reality-headset-xe800zba-hc1us/)

Portable Acer [Détails](https://www.acer.com/ac/en/US/content/model/VD.R05AP.002)

Si votre emplacement est spécialisé dans des expériences de réalité mixtes ou augmentées nécessitant l’utilisation d’un casque d’extraction, vous pouvez obtenir le Microsoft HoloLens 2 (à présent ouvert pour des raisons de préordre).  

HoloLens 2: [Préordre des intérêts](https://www.microsoft.com/en-us/hololens/buy)

Si vous expérimentez avec des expériences qui nécessitent une vision avancée de l’ordinateur, le suivi de la parole et du corps, vous trouverez peut-être Azure Kinect DK adapté à vos besoins.  

Kinect Azure: [Détails](https://azure.microsoft.com/en-us/services/kinect-dk/)

**Q : Qu’est-ce que le portefeuille d’ordinateurs de poche que je peux utiliser pour exécuter mes expériences de VR de PC.**

Pour les expériences de VR du PC, nos fabricants d’ordinateurs OEM offrent une sélection incroyable de PC de sac à dos conçus exactement pour ce besoin.

HP vient de lancer son sac à dos HP VR G2, le PC portable le plus puissant au monde: optimisé pour les expériences gratuites-itinérantes, avec une puissance de 30% avec un GPU RTX 2080 à l’intérieur. [Détails](https://www8.hp.com/us/en/vr/vr-backpack.html)

### <a name="setup"></a>Installation

**Q : Comment puis-je configurer plus facilement le programme d’installation et personnaliser le portail de réalité mixte pour LBE?**

>[!NOTE]
>Cette fonctionnalité nécessite la version 2000.19061.1011.0 ou ultérieure.  

Il se peut que vous ayez besoin de plus de personnalisation du portail de réalité mixte que ce qui est normalement disponible via l’application pour déployer des applications sur des bornes ou des expériences personnalisées. La dernière mise à jour de juillet du portail de réalité mixte prend en charge plusieurs paramètres avancés qui peuvent être via un fichier de configuration pour effectuer les opérations suivantes:  

Autoriser les vérifications système en échec: normalement, le processus d’installation vérifie la compatibilité du PC avec Windows Mixed Reality avant de terminer l’installation. Si vous ignorez cela, vous risquez de rencontrer des problèmes lors de la tentative d’exécution de Windows Mixed Reality en cas de problème de compatibilité.  

Ignorer l’application compagnon de l’appareil: le DCA fournit des étapes de configuration spécifiques au casque fournies par le fabricant et permet de mettre à jour le microprogramme du casque.  

Ignorer la configuration de la salle: au lieu d’être invité à créer une limite de salle, vous pouvez passer directement au casque en mode assis/debout.  

Ignorer l’installation d’applications à partir du Store: le programme d’installation normale installe plusieurs applications du Windows Store, notamment la visionneuse 3D et le module complémentaire de la visionneuse Edge 360. Cela va ignorer l’installation de ces applications, mais il se peut que vous manquiez des fonctionnalités d’appareil.  

Afficher l’aperçu en mode plein écran: le portail de réalité mixte affiche par défaut la préversion du casque en mode plein écran sur le PC de bureau pendant que le casque est en cours d’utilisation.  

Masquer le nouveau volet pour vous: cela empêche le nouveau panneau pour vous d’être développé au lancement du portail de réalité mixte.  

#### <a name="how-to-configure"></a>Procédure de configuration :  

Pour définir l’une de ces configurations, vous devez créer un fichier appelé _userconfig. JSON_ sous ce répertoire: _\\ $env: LOCALAPPDATA\Packages\Microsoft.MixedReality.Portal_8wekyb3d8bbwe\LocalState_

Pour la plupart des utilisateurs, cela ressemble à _C:\Users\<nom_utilisateur\\ > \AppData\Local\Packages\microsoft.mixedreality.portal_8wekyb3d8bbwe\LocalState_

Le fichier JSON doit avoir le contenu ci-dessous avec «true» défini pour l’un des paramètres ci-dessus que vous souhaitez activer:  

```
{

  "shouldAllowFailedSystemChecks": true,

  "shouldSkipDcaApp": true,

  "shouldSkipRoomSetup": true,

  "shouldSkipStoreAppInstall": true,

  "shouldShowPreviewFullScreen": true,

  "shouldHideEngagementPane": true

}
```
 
**Q : Existe-t-il des instructions sur la configuration du PlaySpace?**

R : La configuration d’un Playspace doit être effectuée comme vous le feriez avec une expérience d’installation du consommateur. Le processus de configuration de la salle vous permet également de définir les limites de votre salle. Vous trouverez plus d’informations sur la configuration des limites de la salle [ici](https://docs.microsoft.com/en-us/windows/mixed-reality/enthusiast-guide/set-up-windows-mixed-reality#set-up-your-room-boundary).

Comme indiqué dans le document ci-dessus, la coordonnée unique raisonnable PlaySpace est autour de 5mx5m. Si vous souhaitez disposer d’une plus grande surface, vous pouvez utiliser la fonctionnalité d’ancrages spatiaux dans la pile d’API holographique Windows. L’utilisation de cette API nécessite une ingénierie personnalisée dans les expériences que vous produisez.  

Pour plus d’informations sur l’optimisation de votre contenu en fonction de la taille de l’espace, consultez [cette page](https://docs.microsoft.com/en-us/windows/mixed-reality/coordinate-systems).
 

**Q : Mon espace est trop grand et je rencontre des erreurs lorsque j’essaie de configurer une expérience permanente avec les limites. Que dois-je faire pour configurer mon expérience d’itinérance gratuite?**

R : Pour configurer un espace plus grand que ~ 18x18ft, vous ne pouvez pas utiliser l’expérience de limite fournie par le système.  Les systèmes de limites s’appuient sur l’utilisation d’une «ancre» de coordonnée fixe, qui peut devenir instable lorsqu’un utilisateur est trop éloigné de l’ancre d’étape centrale. 

Au lieu de cela, vous pouvez configurer le mode «assiste», qui n’affiche pas la limite ou ne configure pas les limites d’un étage ou PlaySpace.  Ensuite, vous devez configurer plusieurs ancres spatiales dans l’application pour référencer les zones de limites physiques. 

Le développeur de l’application est responsable de l’affichage des protections nécessaires afin que les utilisateurs n’entrent pas en conflit avec l’environnement physique.  Il peut s’agir de murs numériques au sein de l’expérience ou d’un visuel de limite de jeu personnalisé. 

Vous trouverez des conseils sur la configuration de la limite de la salle avec WMR [ici](https://docs.microsoft.com/en-us/windows/mixed-reality/enthusiast-guide/set-up-windows-mixed-reality#set-up-your-room-boundary).

**Q : Où se trouve l’origine du PlaySpace?**

R : L’origine du PlaySpace est déterminée par l’expérience d’installation de la salle, plus précisément la position de la HMD lorsque le bouton central est enfoncé pendant l’installation. 

### <a name="multi-player-setup"></a>CONFIGURATION MULTI-JOUEURS

**Q : Je déploie une expérience multi-joueurs dans à mon lieu. La prise en charge de Windows Mixed Reality est-elle prise en charge?**

R : L’outil de package de données spatiales de la réalité mixte est une fonctionnalité bêta qui permet de localiser plusieurs joueurs dans le même espace en activant le portage des données spatiales d’un ordinateur vers un autre. Vous pouvez accéder à l’outil et en savoir plus à ce sujet [ici](mixedrealityspatialdatapackager.md).

### <a name="tracking"></a>SUIVRE

Q : Comment fonctionne la technologie de suivi des casques Windows mixtes de réalité?  

La réalité mixte partage la même technologie de suivi que le HoloLens. Pour en savoir plus sur le système de suivi interne, consultez la documentation [ici](https://docs.microsoft.com/en-us/windows/mixed-reality/enthusiast-guide/tracking-system).

Pour obtenir une description de la façon dont le système de mappage spatial de niveau supérieur fonctionne, vous pouvez lire notre description [ici](spatial-mapping-design.md).

**Q : Existe-t-il des pratiques recommandées pour obtenir un volume de suivi fiable?**

Pour mieux configurer l’environnement pour le suivi des réussites, vous pouvez lire les meilleures pratiques dans ce [billet](environment-considerations-for-hololens.md).

**Q : Existe-t-il des nuances spécifiques avec le suivi des espaces ou des optimisations à l’échelle de l’entrepôt?**

R : Les pratiques suivantes peuvent vous aider à obtenir un volume de suivi plus fiable:  

Le fait de fournir une variété de fonctionnalités dans la salle qui se chevauchent à plusieurs emplacements permet au système de suivi d’obtenir un verrou solide. Considérez les hachures et les hachures aléatoires au lieu d’utiliser des lignes de style de contour solides. 

Réduisez autant que possible la plage dynamique d’éclairage dans votre région. Les caméras de suivi sur notre HMDs de réalité mixte ne sont pas HDR et ont des commandes AGC (gain automatique) et AEC (exposition automatique) pour gérer différents éclairages. En fonction de la répartition de la surface, des motifs et du contraste, AGC ou AEC peut vous conclure que vous vous retrouvez dans une pièce blanche ou noire qui peut nettoyer les fonctionnalités qui peuvent être dans la «couleur» opposée. Si vous essayez de prendre une image intérieure devant une fenêtre extérieure avec une lumière de l’heure d’été et que vous ajustez l’exposition pour voir les détails en dehors de, tout ce qui se trouve à l’intérieur est sous-exposé et noir. Ou, s’il est défini à l’intérieur de, tout ce qui est à l’extérieur est maintenant surexposé et tout blanc.  

Des lumières dans une pièce (même des surcharges) qui sont en vue si le suivi des caméras peut parfois être à l’origine de la confusion de l’AEC/AGC des caméras de suivi. L’éclairage plat/diffus vous aide.  

### <a name="mixed-reality-cloud-services-and-azure"></a>SERVICES CLOUD DE RÉALITÉ MIXTE ET AZURE 

**Q : Comment Microsoft Azure aider à mon entreprise?**

R : La gestion sur site et à distance basée sur Azure peut aider votre entreprise à être pilotée par les données, à réduire les coûts d’exploitation et à mettre à l’échelle le déploiement sur les sites existants et nouveaux. Les services de Cloud Computing Azure, tels que le stockage Azure, Azure Functions, App Service, la mise en réseau Azure et IOT Hub peuvent vous aider dans les cas d’utilisation suivants:  

Gestion des & de déploiement des appareils à distance 

Analyses sur site en temps réel 

Jeu intelligent LBE adaptatif 

Diffusion et déploiement de contenu LBE 

LBE de préférence du lecteur carte thermique 

Système de réservation et de réservation LBE 

**Q : Je développe un MMOG spatial à déployer sur un encombrement énorme. Tous les services qui m’aident à gérer mon contenu et la persistance des objets?**

R : Les ancres spatiales Azure sont un nouveau service de réalité mixte qui permet l’utilisation de la réalité mixte multi-utilisateur, avec prise en charge spatiale, sur les appareils HoloLens, iOS et Android. Vous pouvez en savoir plus sur les ancres spatiales Azure [ici](https://azure.microsoft.com/en-us/services/spatial-anchors/).

**Q. Notre lieu est spécialisé dans les expériences multi-joueurs et je souhaite concentrer notre temps de développement sur le contenu et le développement frontal. Existe-t-il des offres qui peuvent m’aider à démarrer ou à décharger le développement principal?**

R : Azure PlayFab est une plateforme backend complète pour les jeux en direct. Vous pouvez en savoir plus à ce sujet [ici](https://playfab.com/).

### <a name="misc"></a>Divers

**Q : J’utilise SteamVR pour déployer mes expériences. Windows Mixed Reality fonctionne-t-il avec SteamVR?**

R : Windows Mixed Reality for SteamVR permet aux utilisateurs d’exécuter des expériences SteamVR sur des casques immersifs immersifs de Windows Mixed Reality. En savoir plus sur SteamVR avec WMR [ici](https://docs.microsoft.com/en-us/windows/mixed-reality/enthusiast-guide/using-steamvr-with-windows-mixed-reality).

### <a name="support-and-community"></a>Support et communauté  

Voici quelques ressources utiles pour faire appel à des experts de notre équipe, obtenir un support de dépannage et contribuer à la communauté de développement de la réalité mixte.  

Si vous rencontrez des problèmes avec les fonctionnalités publiées publiquement, signalez un bogue à l’aide de feedback Hub. pour obtenir de l’aide, reportez-vous à cette [page](https://docs.microsoft.com/en-us/windows/mixed-reality/enthusiast-guide/filing-feedback).

Pour obtenir une aide supplémentaire sur la résolution des problèmes avec WMR, contactez notre équipe de support technique en soumettant une [demande de support](https://support.microsoft.com/en-us/supportforbusiness/productselection?sapId=96bfb202-bc79-741b-bf7a-774d8b767782).

Participez à notre canal HoloDevelopers pour collaborer avec les développeurs travaillant sur la réalité mixte et les experts de l’équipe: [aka.ms/holodevelopers](https://aka.ms/holodevelopers)

Twitter Suivez notre équipe de relations développeurs de réalité mixte pour les actualités, les événements et les mises à jour@MxdRealityDev 

Si vous êtes en déplacement ou autour de San Francisco, il y a toujours un problème qui se passe sur le réacteur Microsoft. Vous pouvez voir notre calendrier d’événements [ici](https://developer.microsoft.com/en-us/reactor/Location/San%20Francisco).