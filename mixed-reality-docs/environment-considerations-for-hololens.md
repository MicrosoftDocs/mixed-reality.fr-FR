---
title: Considérations sur l’environnement pour HoloLens
description: Obtenir la meilleure expérience possible à l’aide de HoloLens lorsque vous optimisez l’appareil pour votre environnement et les yeux. Plusieurs facteurs environnementaux sont fusionnés entre eux pour activer le suivi, mais un développeur de réalité mixte, il existe plusieurs facteurs vous pouvez prendre en compte pour régler un espace pour une meilleure hologrammes.
author: dorreneb
ms.author: dobrown
ms.date: 04/22/2019
ms.topic: article
keywords: frame HOLOGRAPHIQUE, champ de vision, angle d’ouverture, étalonnage, espaces, environnement, procédure
ms.openlocfilehash: 0070455792e09cd59741362b201ca6b7b9af0aec
ms.sourcegitcommit: f5c1dedb3b9e29f27f627025b9e7613931a7ce18
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64670174"
---
# <a name="environment-considerations-for-hololens"></a>Considérations sur l’environnement pour HoloLens

HoloLens fusionne le holographique avec le monde « réel », plaçant hologrammes dans votre environnement. Une fenêtre d’application HOLOGRAPHIQUE « se bloque » sur le mur, une ballerine HOLOGRAPHIQUE tourne sur le bureau, les oreilles lapin se trouvent en haut de la tête de votre ami à son insu. Lorsque vous utilisez un jeu immersive ou votre application, le monde HOLOGRAPHIQUE répartit pour remplir votre environnement, mais vous serez toujours en mesure de voir et vous déplacer dans l’espace.

Les hologrammes que vous placer reste où vous avez placez-les, même si vous désactivez votre appareil. 

## <a name="setting-up-an-environment"></a>Configuration d’un environnement

Les appareils HoloLens savent comment placer hologrammes stables et précises par *suivi* les utilisateurs dans un espace. Sans suivi approprié, l’appareil ne comprend pas l’environnement ou l’utilisateur qu’il contient - hologrammes peuvent apparaître dans les mauvais endroits, apparaissent pas dans la même chaque fois ou apparaît pas du tout.

Suivi des performances, fortement influencé par l’environnement de que l’utilisateur est membre et induire un suivi stable et cohérent dans un environnement de paramétrage est un art, et non une science. Plusieurs facteurs environnementaux sont fusionnés entre eux pour activer le suivi, mais un développeur de réalité mixte, il existe plusieurs facteurs vous pouvez prendre en compte pour régler un espace pour améliorer leur suivi.
 
### <a name="lighting"></a>Éclairage
Réalité mixte Windows utilise light visuel pour effectuer le suivi d’emplacement de l’utilisateur. Lorsqu’un environnement est trop clair, les caméras peuvent être saturées, et rien ne s’affiche. Si l’environnement est trop foncé, les caméras de surveillance ne peut pas récupérer suffisamment d’informations, et rien ne se produit. Éclairage doit être la même et suffisamment clair qu’un humain peut voir sans effort, mais pas par conséquent, luminosité que la lumière est pénible à examiner.

Zones où il y a points de lumière dans une zone globale dim sont également problématiques, car l’appareil photo doit ajuster lors du déplacement et l’extraction d’espaces vives. Cela peut entraîner l’appareil « obtenir perdu » et pense que la modification de la lumière équivaut à un changement d’emplacement. Niveau d’éclairage stable dans une zone conduira à améliorer leur suivi.

N’importe quel éclairage extérieur peut également entraîner une instabilité dans le dispositif de suivi, comme le soleil peut varier considérablement au fil du temps. Par exemple, le suivi dans le même espace de l’été et hiver peut produire des résultats considérablement différents, comme la lumière secondhand à l’extérieur peut-être être supérieure à différents moments de l’année.

Si vous avez un luxmeter, un lux de 500 à 1000 stable est un bon point de départ. 

#### <a name="types-of-lighting"></a>Types d’éclairage
Différents types de lumière dans un espace peuvent également influencer le suivi. Ampoules impulsions avec l’électricité AC en - si la fréquence de CA est de 50Hz, puis la lumière se propage à 50Hz. Pour un humain, cette impulsion n’est pas remarqué. Toutefois, appareil photo de 30 i/s des HoloLens voit ces modifications - certaines images seront bien éclairés certaines seront allumée mal et certaines seront excessif exposées comme tente de l’appareil photo compenser des impulsions de lumière.

Aux États-Unis d’Amérique, fréquence d’électricité standard étant 60Hz, lightbulb pulsations sont harmonisées avec une fréquence d’images des HoloLens - 60Hz impulsions s’aligner avec une fréquence d’images des Hololens 30 i/s. Toutefois, dans de nombreux pays ont une norme de fréquence CA 50 Hz, ce qui signifie que certaines trames Hololens seront prises lors des pulsations, et d’autres pas. En particulier, FLUORESCENTS en Europe a connus pour provoquer des problèmes. 

Il existe quelques éléments que vous pouvez essayer de résoudre les problèmes de scintillement. Température, l’âge de l’ampoule et cycles de mise en route sont des causes courantes de scintillement fluorescent et en remplaçant les ampoules peut être utile. Renforcement des ampoules et assurant dessine actuel est constants peuvent également aider. 

### <a name="items-in-a-space"></a>Éléments dans un espace
HoloLens utilise des points d’intérêt l’environnement uniques, également appelé *fonctionnalités*, pour localiser lui-même dans un espace. 

Un appareil peut suivre presque jamais dans une zone de fonctionnalité-médiocre, comme l’appareil n’a aucun moyen de savoir où dans l’espace qu’il est. Ajout de fonctionnalités pour les murs d’un espace est généralement un bon moyen d’améliorer le suivi. Affiches, symboles tapés sur un mur, des usines, des objets uniques ou d’autres éléments similaires toute l’aide. Un support désordonné est un bon exemple d’un environnement qui mène à bon suivi : il existe de nombreuses fonctionnalités différentes dans une seule zone. 

En outre, utilisent des fonctionnalités uniques dans le même espace. Le même poster répétée plusieurs fois sur un mur, par exemple, provoquent confusion de l’appareil comme le HoloLens ne saura pas parmi les posters répétitives, il consulte. Une méthode courante d’ajout de fonctionnalités uniques consiste à utiliser les lignes de la bande à créer unique, modèles nonrepetitve le long des murs et étage d’un espace. 

Une bonne question à poser est : Si vous l’avez vu juste une petite quantité de la scène, pouvez vous identifie de façon unique localiser vous-même dans l’espace ? Si ce n’est pas le cas, il est probable que le périphérique aura le suivi des problèmes.

#### <a name="wormholes"></a>Ver géant
Si vous avez deux zones ou des régions qui ont le même aspect, le dispositif de suivi peut penser qu’ils sont identiques. Il en résulte l’appareil lui-même amenant à penser que cela est un autre emplacement. Nous appelons ces types de zones répétitives *ver géant*. 

Pour empêcher le ver géant, essayez afin d’éviter les zones identiques dans le même espace. Parfois, les zones identiques peuvent inclure des stations de fabrique, windows sur un bâtiment, racks de serveurs ou stations de travail. Étiquetage des zones ou en ajoutant des fonctionnalités uniques à chaque zones similaires peut aider à atténuer ver géant.
 
### <a name="temporal-stability-of-a-space"></a>Stabilité temporelle d’un espace
Si votre environnement est en permanence un décalage et la modification, l’appareil n’a aucune fonctionnalité stable à localiser sur. 

Les objets de déplacer davantage qui se trouvent dans un espace, y compris les personnes, plus il est facile de perdre le suivi. Déplacement tapis roulants, des éléments dans les différents États de la construction et un grand nombre de personnes dans un espace ont tous connus pour provoquer des problèmes de suivi.
 
### <a name="proximity-of-the-user-to-items-in-the-space"></a>Proximité de l’utilisateur aux éléments dans l’espace
De même pour comment l’homme est impossible d’analyser correctement sur les objets proches du point de vue, HoloLens avez-vous du mal lorsque les objets sont proches de caméras. Si un objet est trop étroite pour être vu avec les deux caméras, ou si un objet bloque un appareil photo, le périphérique aura beaucoup plus de problèmes avec le suivi par rapport à l’objet. 

Les caméras peuvent voir ne moins de 15cm à partir d’un objet.
 
### <a name="surfaces-in-a-space"></a>Surfaces dans un espace
Surfaces fortement RÉFLÉCHISSANTS aura probablement un aspect différents en fonction de l’angle, ce qui affecte le suivi. Considérez une toute nouvelle voiture - lorsque vous y déplacer, reflète de lumière et vous voyez différents objets dans la surface à mesure que vous déplacez. Au dispositif de suivi, les différents objets répercutées dans l’aire de conception représentent un environnement en constante évolution, et le périphérique perd le suivi.

Moins brillants objets sont plus faciles à suivre par rapport.

### <a name="wifi-fingerprint-considerations"></a>Considérations sur les empreintes digitales de Wi-Fi
Tant que Wi-Fi est activée, les données de mappage seront en corrélation avec une empreinte digitale Wi-Fi, même si ne pas connecté à un réseau Wi-Fi réelle/routeur. Sans informations de Wi-Fi, l’espace et hologrammes peuvent être légèrement plus lentes à reconnaître. Si les signaux Wi-Fi changer de manière significative, l’appareil peut considérer qu’il est complètement dans un autre espace.

Identification de réseau (par exemple, le SSID, adresse MAC) ne sont pas envoyées à Microsoft et Wi-Fi toutes les références sont gardées en locales sur le HoloLens.

## <a name="mapping-new-spaces"></a>Nouveaux espaces de mappage
Lorsque vous entrez un nouvel espace (ou chargez un existant), vous verrez un graphique de maille répartissant dans l’espace. Cela signifie que votre appareil est [votre environnement de mappage](spatial-mapping-design.md). 

Si vous ne parvenez pas à placer hologrammes, essayez de vous épargne l’espace pour HoloLens pouvez mapper plus en détail. 

Si votre HoloLens Impossible de mapper votre espace ou est en dehors de l’étalonnage, vous pouvez entrer le mode Limited. En mode limité, vous ne pourrez pas placer hologrammes dans votre environnement.

## <a name="environment-management"></a>Gestion de l’environnement
Il existe deux paramètres qui permettent aux utilisateurs pour « nettoyer » hologrammes et cause HoloLens d’un espace « oublier ».  Ils existent dans « Hologrammes et environnements » dans l’application paramètres, avec le deuxième paramètre qui apparaît également sous « Confidentialité » dans l’application paramètres.

1.  Suppression de proximité hologrammes : Si vous sélectionnez ce paramètre, HoloLens effacera hologrammes tout ancrés et toutes les données de carte stockées pour « espace actuelle » où se trouve l’appareil.  Une nouvelle section de mappage est créée et stockée dans la base de données pour cet emplacement une fois hologrammes sont placées à nouveau dans le même espace.

2.  Supprimer tous les hologrammes : en sélectionnant ce paramètre, HoloLens effacera toutes ses données de carte et les ancrée hologrammes dans les bases de données entières d’espaces.  Aucun hologrammes ne seront encore détectés et n’importe quel hologrammes doivent être qui vient d’être placés pour stocker à nouveau des sections de la carte dans la base de données.

### <a name="managing-your-spaces"></a>La gestion de vos espaces

Les sections de la carte et les différents espaces ont été réduites dans une base de données, stocké localement sur l’appareil HoloLens. La base de données de mappage est stockée en toute sécurité, avec accès uniquement disponible pour le système interne et jamais à un utilisateur de l’appareil, même lorsqu’un PC connecté et/ou à l’aide de l’application de l’Explorateur de fichiers. Lorsque bitlocker est activé, les données de carte stockées sont également chiffrées.

Plusieurs composants de cartographie existent lorsque hologrammes sont placés dans différents emplacements sans un chemin d’accès de connexion entre les emplacements/hologrammes.  Hologrammes ancrées au sein de la même section de mappage sont considérés comme « proches » dans l’espace en cours.

Il existe une API de développeur pour exporter un petit sous-ensemble de « l’espace en cours » (une partie du composant de mappage qui est actuellement reconnu) pour permettre des scénarios de hologramme partagé.  Il n’existe actuellement aucun mécanisme pour télécharger la base de données de tous les espaces qui ont été mappés.


## <a name="hologram-quality"></a>Qualité de HOLOGRAMME

Hologrammes peuvent être placées dans tout votre environnement : haute, basse et tout autour de vous, mais vous les verrez un [frame HOLOGRAPHIQUE](holographic-frame.md) qui se trouve devant les yeux. Pour obtenir un meilleur affichage, veillez à ajuster votre appareil afin que vous puissiez voir la trame entière. Et n’hésitez pas à parcourir votre environnement et explorez !

Pour votre [hologrammes](hologram.md) pour rechercher clair, clair et stable, votre HoloLens doit être étalonnée rien que pour vous. Lorsque vous configurez tout d’abord votre HoloLens, vous serez guidé dans ce processus. Par la suite si hologrammes ne s’affichent pas correctement ou que vous voyez un grand nombre d’erreurs, vous pouvez effectuer des ajustements.

### <a name="calibration"></a>Étalonnage

Si votre hologrammes regardez instable ou saccadées, ou si vous ne parvenez pas à placer hologrammes, la première chose à faire la [étalonnage application](calibration.md). Cette application peut également utile si vous êtes confronté à toute gêne lors de l’utilisation de votre HoloLens.

Pour accéder à l’application d’étalonnage, accédez à Paramètres > système > Utilitaires. Sélectionnez Ouvrir étalonnage et suivez les instructions.

Si vous exécutez l’application de l’étalonnage et que vous rencontrez toujours des problèmes avec une qualité HOLOGRAMME, ou que vous voyez un message « suivi perdues » fréquentes, essayez l’application de réglage du capteur. Accédez à Paramètres > système > Utilitaires, sélectionnez le paramétrage de capteur ouvert, puis suivez les instructions.

Si quelqu'un d’autre doit être à l’aide de votre HoloLens, il doit s’exécuter l’application d’étalonnage tout d’abord afin de l’appareil est correctement configuré pour eux.

## <a name="see-also"></a>Voir aussi
* [Conception du mappage spatial](spatial-mapping-design.md)
* [Hologrammes](hologram.md)
* [Étalonnage](calibration.md)
