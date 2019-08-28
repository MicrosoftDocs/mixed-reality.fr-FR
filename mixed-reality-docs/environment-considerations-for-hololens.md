---
title: Considérations environnementales pour HoloLens
description: Profitez de la meilleure expérience possible avec HoloLens lorsque vous optimisez l’appareil pour vos yeux et votre environnement. De nombreux facteurs environnementaux différents sont fusionnés pour permettre le suivi, mais en tant que développeur de réalité mixte, il existe plusieurs facteurs que vous pouvez garder à l’esprit pour paramétrer un espace pour de meilleurs hologrammes.
author: dorreneb
ms.author: dobrown
ms.date: 04/22/2019
ms.topic: article
keywords: cadre holographique, champ de vision, angle de fonctionnement, étalonnage, espaces, environnement, procédure
ms.openlocfilehash: cc856c42aaf4ddfca8365f63ab0c7df1a1a3b248
ms.sourcegitcommit: 3b32339c5d5c79eaecd84ed27254a8f4321731f1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70047081"
---
# <a name="environment-considerations-for-hololens"></a>Considérations environnementales pour HoloLens

HoloLens fusionne l’holographique avec le monde «réel», en plaçant des hologrammes dans votre environnement. Une fenêtre d’application holographique «se bloque» sur le mur, un Ballerina holographique tourne sur le bureau, les oreilles des lapins s’appuient sur la tête de votre ami involontaire. Lorsque vous utilisez un jeu ou une application immersif, le monde holographique se répandra pour combler votre environnement, mais vous pourrez toujours voir et vous déplacer dans l’espace.

Les hologrammes que vous placez restent là où vous les avez placés, même si vous éteignez votre appareil. 

## <a name="setting-up-an-environment"></a>Configuration d’un environnement

Les appareils HoloLens savent comment placer des hologrammes stables et précis en effectuant le *suivi* des utilisateurs dans un espace. Si le suivi n’est pas correct, l’appareil ne comprend pas l’environnement ou l’utilisateur au sein de celui-ci. les hologrammes peuvent donc apparaître dans les mauvais endroits, ne pas apparaître dans le même emplacement à chaque fois, ou ne pas apparaître du tout. Les données utilisées pour suivre les utilisateurs sont représentées dans la *carte spatiale*. 

Le suivi des performances est fortement influencé par l’environnement dans lequel se trouve l’utilisateur et le paramétrage d’un environnement pour induire un suivi stable et cohérent est un art plutôt qu’une science. De nombreux facteurs environnementaux différents sont fusionnés pour permettre le suivi, mais en tant que développeur de réalité mixte, vous pouvez garder à l’esprit plusieurs facteurs pour paramétrer un espace afin d’améliorer le suivi.
 
### <a name="lighting"></a>Éclairage
Windows Mixed Reality utilise le visuel clair pour suivre l’emplacement de l’utilisateur. Lorsqu’un environnement est trop brillant, les caméras peuvent être saturées et rien ne s’affiche. Si l’environnement est trop sombre, les caméras ne peuvent pas récupérer suffisamment d’informations et rien ne s’affiche. L’éclairage doit être même et suffisamment lumineux qu’un homme peut voir sans effort, mais pas tellement brillant que la lumière est pénible à regarder.

Les zones où il y a des points de lumière intense dans une zone lumineuse globale sont également problématiques, car l’appareil photo doit s’ajuster lors du déplacement et de la sortie des espaces brillants. Cela peut entraîner la perte de l’appareil et penser que la modification de la lumière équivaut à une modification de l’emplacement. Des niveaux de lumière stables dans une zone permettront d’améliorer le suivi.

Tout éclairage extérieur peut également provoquer une instabilité dans le dispositif de suivi, car le soleil peut varier considérablement dans le temps. Par exemple, le suivi dans le même espace au niveau de l’été et de l’hiver peut produire des résultats radicalement différents, car la lumière Secondhand à l’extérieur peut être plus élevée à différents moments de l’année.

Si vous avez un luxmeter, un 500-1000 lux stable est un bon point de départ. 

#### <a name="types-of-lighting"></a>Types d’éclairage
Les différents types de lumière dans un espace peuvent également influencer le suivi. Les ampoules sont en impulsions avec l’électricité courant à travers le courant: si la fréquence de l’AC est 50Hz, la lumière clignote à 50Hz. Pour un homme, cette pulsation n’est pas remarquée. Toutefois, l’appareil photo 30fps de HoloLens voit ces modifications. certaines images sont bien éclairées, certaines sont mal éclairées, et d’autres sont surexposées lorsque l’appareil photo tente de compenser les impulsions légères.

Aux États-Unis, la norme de fréquence électrique est 60 Hz, de sorte que les impulsions d’ampoule sont harmonisées avec les impulsions de fréquence d’images de HoloLens, alignées avec la cadence de la fréquence de 30 i/s. Toutefois, de nombreux pays ont une norme de fréquence AC de 50Hz, ce qui signifie que certaines images HoloLens seront prises pendant les impulsions, et d’autres non. En particulier, l’éclairage fluorescent en Europe a été connu pour causer des problèmes. 

Vous pouvez essayer de résoudre les problèmes de scintillement en quelques étapes. La température, l’âge des bulbes et les cycles de préchauffage sont des causes courantes du scintillement fluorescent et le remplacement des ampoules peut aider. Il peut également être utile d’alserrer les ampoules et de s’assurer que les dessins actuels sont constants. 

### <a name="items-in-a-space"></a>Éléments dans un espace
HoloLens utilise des points de repère environnementaux uniques, également appelés *fonctionnalités*, pour se trouver dans un espace. 

Un appareil ne peut pratiquement jamais effectuer de suivi dans une zone de fonctionnalité médiocre, car l’appareil n’a aucun moyen de savoir où il est dans l’espace. L’ajout de fonctionnalités aux murs d’un espace est généralement un bon moyen d’améliorer le suivi. Toutes les lignes de l’affiches, les symboles sur bande, les plantes, les objets uniques ou autres éléments similaires. Un bureau en désordre est un bon exemple d’environnement qui donne un bon suivi: il existe de nombreuses fonctionnalités différentes dans une seule zone. 

En outre, utilisez des fonctionnalités uniques dans le même espace. La même affiche répétée plusieurs fois sur un mur, par exemple, entraîne la confusion de l’appareil, car le HoloLens ne sait pas laquelle des affiches répétitives qu’elle examine. Une façon courante d’ajouter des fonctionnalités uniques consiste à utiliser des lignes de masquage de bande pour créer des modèles uniques et non répétitifs le long des murs et de l’étage d’un espace. 

Une bonne question à vous poser est: Si vous avez vu juste une petite partie de la scène, pouvez-vous vous trouver dans l’espace? Si ce n’est pas le cas, il est probable que l’appareil aura également des problèmes de suivi.

#### <a name="wormholes"></a>Repères
Si vous avez deux zones ou régions qui semblent identiques, le dispositif de suivi peut penser qu’elles sont identiques. Cela permet à l’appareil de se tromper pour penser qu’il s’agit d’un autre emplacement. Nous appelons ces types de repères de zone répétitives. 

Pour éviter les repères, essayez d’éviter les zones identiques dans le même espace. Les zones identiques peuvent parfois inclure des stations de fabrique, des fenêtres sur un bâtiment, des racks de serveurs ou des stations de travail. L’étiquetage des zones ou l’ajout de fonctionnalités uniques à chaque zone d’aspect similaire peut aider à atténuer les repères.

### <a name="qr-codes-in-environments"></a>Codes QR dans les environnements.
HoloLens peut utiliser des [codes QR](qr-code-tracking.md) pour plusieurs raisons, par exemple pour étiqueter des objets ou pour fournir un contexte supplémentaire aux environnements, mais ils peuvent également être utilisés pour améliorer la qualité du suivi. HoloLens utilisera automatiquement les codes QR pour faciliter la création d’une carte, même si vous ne consommez pas les données incorporées dans les codes.

Si vous utilisez des codes QR pour faciliter le suivi, vous aurez besoin de deux à trois codes dans un champ de vue donné. Pour de nombreux scénarios, cela se traduit par la mise en place d’un code QR tous les 2-3 ou 6-9 mètres.

Assurez-vous que les codes QR sont plats et fermement attachés aux murs ou à d’autres surfaces.

Les meilleures pratiques pour la génération et l’impression de codes QR se trouvent dans [meilleures pratiques pour la détection du code QR](qr-code-tracking.md#best-practices-for-qr-code-detection).
 
### <a name="movement-in-a-space"></a>Déplacement dans un espace
Si votre environnement est en constante évolution et change, l’appareil n’a pas de fonctionnalités stables à rechercher. 

Plus les objets mobiles sont présents dans un espace, y compris les personnes, plus il est facile de perdre le suivi. Les tapis roulants, les éléments dans différents États de construction et un grand nombre de personnes dans un espace ont tous été connus pour provoquer des problèmes de suivi.

Le HoloLens peut rapidement s’adapter à ces modifications, mais uniquement lorsque cette zone est clairement visible pour l’appareil. Les zones qui ne sont pas considérées comme fréquentes peuvent avoir un retard en arrière-plan, ce qui peut provoquer des erreurs dans la carte spatiale. Par exemple, un utilisateur balaie un ami, puis se contourne alors que l’ami quitte la salle. Une représentation «fantôme» de l’ami est conservée dans les données de mappage spatiale jusqu’à ce que l’utilisateur relance l’analyse de l’espace vide.
 
### <a name="proximity-of-the-user-to-items-in-the-space"></a>Proximité de l’utilisateur aux éléments de l’espace
De même que la façon dont les êtres humains ne peuvent pas se concentrer bien sur les objets à proximité des yeux, HoloLens éprouve des difficultés quand les objets sont proches des appareils photo. Si un objet est trop proche pour être visible avec les deux caméras, ou si un objet bloque un appareil photo, l’appareil rencontre beaucoup plus de problèmes avec le suivi de l’objet. 

Les caméras ne peuvent pas voir plus près que 15cm d’un objet.
 
### <a name="surfaces-in-a-space"></a>Surfaces dans un espace
Les surfaces fortement réfléchissantes auront probablement un aspect différent selon l’angle, ce qui affecte le suivi. Imaginez une toute nouvelle voiture: quand vous la déplacez, la lumière reflète et vous voyez différents objets dans la surface au fur et à mesure que vous déplacez. Dans le dispositif de suivi, les différents objets reflétés dans la surface représentent un environnement changeant, et l’appareil perd le suivi.

Les objets moins brillants sont plus faciles à suivre.

### <a name="wifi-fingerprint-considerations"></a>Considérations sur les empreintes digitales
Tant que le Wi-Fi est activé, les données cartographiques sont corrélées avec une empreinte Wi-Fi, même si elles ne sont pas connectées à un réseau/routeur Wi-Fi réel. Sans les informations WiFi, l’espace et les hologrammes peuvent être légèrement plus lents à reconnaître. Si les signaux WiFi changent de manière significative, l’appareil peut penser qu’il se trouve dans un autre espace.

L’identification réseau (par exemple, SSID, adresse MAC) n’est pas envoyée à Microsoft, et toutes les références WiFi sont conservées localement sur le HoloLens.

## <a name="mapping-new-spaces"></a>Mappage de nouveaux espaces
Lorsque vous entrez un nouvel espace (ou chargez un espace existant), un graphique maillé s’étale sur l’espace. Cela signifie que votre appareil est en mode de mappage de votre environnement. Alors qu’un HoloLens apprend un espace dans le temps, il y a des [trucs et astuces pour mapper les espaces](use-hololens-in-new-spaces.md). 

## <a name="environment-management"></a>Gestion de l’environnement
Il existe deux paramètres qui permettent aux utilisateurs de «nettoyer» les hologrammes et de faire en sorte que HoloLens «oublie» un espace.  Ils se trouvent dans «hologrammes et environnements» dans l’application paramètres, le deuxième paramètre apparaissant également sous «confidentialité» dans l’application paramètres.

1.  Supprimer les hologrammes à proximité: en sélectionnant ce paramètre, HoloLens efface tous les hologrammes ancrés et toutes les données cartographiques stockées pour l’espace actuel dans lequel se trouve l’appareil.  Une nouvelle section de mappage est créée et stockée dans la base de données pour cet emplacement une fois les hologrammes placés dans le même espace.

2.  Supprimer tous les hologrammes: en sélectionnant ce paramètre, HoloLens efface toutes les données cartographiques et les hologrammes ancrés dans l’ensemble des bases de données d’espaces.  Aucun hologramme n’est redécouvert et tous les hologrammes doivent être placés à nouveau pour stocker les sections de mappage dans la base de données.


## <a name="hologram-quality"></a>Qualité de l’hologramme

Les hologrammes peuvent être placés dans l’ensemble de votre environnement (haute, faible, etc.), mais vous les verrez par le biais d’un [cadre holographique](holographic-frame.md) qui se trouve devant vos yeux. Pour obtenir la meilleure vue, veillez à ajuster votre appareil pour que vous puissiez voir le frame entier. Et n’hésitez pas à vous familiariser avec votre environnement et à explorer!

Pour que vos [hologrammes](hologram.md) soient nets, clairs et stables, votre HoloLens doit être calibré juste pour vous. Quand vous configurez pour la première fois votre HoloLens, vous serez guidé tout au long de ce processus. Plus tard, si les hologrammes ne s’affichent pas correctement ou si vous voyez de nombreuses erreurs, vous pouvez effectuer des ajustements.

Si vous avez des difficultés à mapper des espaces, essayez de supprimer les hologrammes à proximité et de remapper l’espace.

### <a name="calibration"></a>Auto

Si vos hologrammes semblent instables ou tremblent, ou si vous avez des difficultés à placer des hologrammes, la première chose à essayer est l' [application d’étalonnage](calibration.md). Cette application peut également être utile si vous rencontrez des problèmes lors de l’utilisation de votre HoloLens.

Pour accéder à l’application d’étalonnage, accédez à paramètres > les utilitaires du > système. Sélectionnez ouvrir l’étalonnage et suivez les instructions.

Si vous exécutez l’application d’étalonnage et que vous rencontrez toujours des problèmes de qualité d’hologramme, ou que vous voyez un message «suivi perdu» fréquent, essayez l’application de réglage du capteur. Accédez à paramètres > les utilitaires du > système, sélectionnez Ouvrir le réglage du capteur et suivez les instructions.

Si quelqu’un d’autre utilise votre HoloLens, il doit d’abord exécuter l’application d’étalonnage pour que l’appareil soit configuré correctement.

## <a name="see-also"></a>Voir aussi
* [Conception du mappage spatial](spatial-mapping-design.md)
* [Hologrammes](hologram.md)
* [Étalonnage](calibration.md)
* [Utiliser HoloLens dans de nouveaux espaces](use-hololens-in-new-spaces.md)
