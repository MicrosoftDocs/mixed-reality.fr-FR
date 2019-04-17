---
title: Considérations sur l’environnement pour HoloLens
description: Obtenir la meilleure expérience possible à l’aide de HoloLens lorsque vous optimisez l’appareil pour votre environnement et les yeux.
author: thetuvix
ms.author: msamples
ms.date: 02/24/2019
ms.topic: article
keywords: frame HOLOGRAPHIQUE, champ de vision, angle d’ouverture, étalonnage, espaces, environnement, procédure
ms.openlocfilehash: d5433dc923aeb70e3ae82e75c9358d3a569e8f83
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59594829"
---
# <a name="environment-considerations-for-hololens"></a>Considérations sur l’environnement pour HoloLens

HoloLens fusionne le holographique avec le monde « réel », plaçant hologrammes dans votre environnement. Une fenêtre d’application HOLOGRAPHIQUE « se bloque » sur le mur, une ballerine HOLOGRAPHIQUE tourne sur le bureau, les oreilles lapin se trouvent en haut de la tête de votre ami à son insu. Lorsque vous utilisez un jeu immersive ou votre application, le monde HOLOGRAPHIQUE répartit pour remplir votre environnement, mais vous serez toujours en mesure de voir et vous déplacer dans l’espace.

Les hologrammes que vous placer reste où vous avez placez-les, même si vous désactivez votre appareil. 

Voici quelques points à prendre en compte pour une expérience optimale avec le monde HOLOGRAPHIQUE. Notez, HoloLens est conçu pour être utilisé à l’intérieur dans un espace sécurisé avec aucun dangers trébucher. Ne pas l’utiliser lors de la conduite ou effectuer d’autres activités qui nécessitent votre attention complète.

## <a name="spaces"></a>Espaces

HoloLens a eu connaissance de votre espace afin qu’il rappeler où vous avez placé hologrammes. HoloLens peuvent se souvenir de plusieurs espaces et est conçu pour charger l’espace approprié lorsque vous l’activez.

### <a name="setting-up"></a>Configuration de

HoloLens peut mapper et n’oubliez pas de vos espaces de mieux si vous choisissez l’environnement approprié.
* Utiliser une salle avec light adéquat et suffisamment d’espace disque. Évitez les espaces foncées et salles avec un grand nombre de surfaces foncées, brillants ou translucides (par exemple, les miroirs ou rideaux mince).
* Si vous souhaitez HoloLens pour en savoir plus un espace, en face directement, d’environ un compteur.
* Évitez les espaces avec un grand nombre d’objets en mouvement. Si un élément a été déplacé et que vous souhaitez HoloLens pour en savoir plus de sa nouvelle position (par exemple, vous avez déplacé votre art vers un nouveau point), utilisation et vous déplacer dans il.

### <a name="spatial-mapping"></a>Mappage spatial

Lorsque vous entrez un nouvel espace (ou chargez un existant), vous verrez un graphique de maille répartissant dans l’espace. Cela signifie que votre appareil est [votre environnement de mappage](spatial-mapping-design.md). Si vous ne parvenez pas à placer hologrammes, essayez de vous épargne l’espace pour HoloLens pouvez mapper plus en détail. Si votre HoloLens Impossible de mapper votre espace ou est en dehors de l’étalonnage, vous pouvez entrer le mode Limited. En mode limité, vous ne pourrez pas placer hologrammes dans votre environnement.

### <a name="managing-your-spaces"></a>La gestion de vos espaces

Les sections de la carte et les différents espaces ont été réduites dans une base de données, stocké localement sur l’appareil HoloLens.  La base de données de mappage est stockée en toute sécurité, avec accès uniquement disponible pour le système interne et jamais à un utilisateur de l’appareil, même lorsqu’un PC connecté et/ou à l’aide de l’application de l’Explorateur de fichiers.  Lorsque bitlocker est activé, les données de carte stockées sont également chiffrées.
Plusieurs composants de cartographie existent lorsque hologrammes sont placés dans différents emplacements sans un chemin d’accès de connexion entre les emplacements/hologrammes.  Hologrammes ancrées au sein de la même section de mappage sont considérés comme étant « proches » dans l’espace actuellement il est une API de développeur pour exporter un petit sous-ensemble de « l’espace en cours » (une partie du composant de mappage qui est actuellement reconnu) pour permettre des scénarios de hologramme partagé.  Il n’existe actuellement aucun mécanisme pour télécharger la base de données de tous les espaces qui ont été mappés.

#### <a name="wifi"></a>WiFi
Visual Studio connecté. Pas – tant que Wi-Fi est activée, les données de mappage seront en corrélation avec une empreinte digitale Wi-Fi, même si ne pas connecté à un réseau Wi-Fi réelle/routeur.  Il s’agit, car le MAC adresse offerte (autrement dit, Wi-Fi empreinte digitale) d’un routeur est disponible sans connexion à celui-ci.  Identification de réseau (par exemple, le SSID, adresse MAC) ne sont pas envoyées à Microsoft et Wi-Fi toutes les références sont gardées en locales sur le HoloLens.

Visual Studio est activée. Désactivé : HoloLens sera sens et n’oubliez pas d’espaces même lorsque Wi-Fi est désactivé, en stockant les données de capteur lorsque hologrammes sont placés.  Sans les informations de Wi-Fi, l’espace et hologrammes peuvent être légèrement plus lentes à reconnaître à une date ultérieure, comme le HoloLens doit comparer les analyses actives à tous les points d’ancrage hologramme et sections de carte stockées sur l’appareil pour « relocalize » à la partie droite de la carte.

#### <a name="environment-management"></a>Gestion de l’environnement
Il existe 2 paramètres qui permettent aux utilisateurs pour « nettoyer » hologrammes et cause HoloLens « oublier un espace ».  Ils existent dans « Hologrammes et environnements » dans l’application paramètres, avec le deuxième paramètre qui apparaît également sous « Confidentialité » dans l’application paramètres.
1.  Suppression de proximité hologrammes : Si vous sélectionnez ce paramètre, HoloLens effacera hologrammes tout ancrés et toutes les données de carte stockées pour « espace actuelle » où se trouve l’appareil.  Une nouvelle section de mappage est créée et stockée dans la base de données pour cet emplacement une fois hologrammes sont placées à nouveau dans le même espace.
2.  Supprimer tous les hologrammes : en sélectionnant ce paramètre, HoloLens effacera toutes ses données de carte et les ancrée hologrammes dans les bases de données entières d’espaces.  Aucun hologrammes ne seront encore détectés et n’importe quel hologrammes doivent être qui vient d’être placés pour stocker à nouveau des sections de la carte dans la base de données.


## <a name="hologram-quality"></a>Qualité de HOLOGRAMME

Hologrammes peuvent être placées dans tout votre environnement : haute, basse et tout autour de vous, mais vous les verrez un [frame HOLOGRAPHIQUE](holographic-frame.md) qui se trouve devant les yeux. Pour obtenir un meilleur affichage, veillez à ajuster votre appareil afin que vous puissiez voir la trame entière. Et n’hésitez pas à parcourir votre environnement et explorez !

Pour votre [hologrammes](hologram.md) pour rechercher clair, clair et stable, votre HoloLens doit être étalonnée rien que pour vous. Lorsque vous configurez tout d’abord votre HoloLens, vous serez guidé dans ce processus. Par la suite si hologrammes ne s’affichent pas correctement ou que vous voyez un grand nombre d’erreurs, vous pouvez effectuer des ajustements.

### <a name="calibration"></a>Étalonnage

Si votre hologrammes regardez instable ou saccadées, ou si vous ne parvenez pas à placer hologrammes, la première chose à faire la [étalonnage application](calibration.md). Cette application peut également utile si vous êtes confronté à toute gêne lors de l’utilisation de votre HoloLens.

Pour accéder à l’application d’étalonnage, accédez à Paramètres > système > Utilitaires. Sélectionnez Ouvrir étalonnage et suivez les instructions.

Si vous exécutez l’application de l’étalonnage et que vous rencontrez toujours des problèmes avec une qualité HOLOGRAMME, ou que vous voyez un message « suivi perdues » fréquentes, essayez l’application de réglage du capteur. Accédez à Paramètres > système > Utilitaires, sélectionnez le paramétrage de capteur ouvert, puis suivez les instructions.

Si quelqu'un d’autre doit être à l’aide de votre HoloLens, il doit s’exécuter l’application d’étalonnage tout d’abord afin de l’appareil est correctement configuré pour eux.

## <a name="see-also"></a>Voir aussi
* [Conception de mappage spatial](spatial-mapping-design.md)
* [Hologrammes](hologram.md)
* [Calibration](calibration.md)
