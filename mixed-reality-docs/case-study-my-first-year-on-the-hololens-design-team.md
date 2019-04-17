---
title: Étude de cas - équipe de conception de ma première année sur l’HoloLens
description: Mon parcours à partir d’un flatland 2D pour le monde en 3D démarré lorsque j’ai rejoint l’équipe de conception de HoloLens en janvier 2016.
author: designnomad
ms.author: haejinl
ms.date: 03/21/2018
ms.topic: article
keywords: Personnel éditorial, de conception, Windows Mixed Reality, HoloLens,
ms.openlocfilehash: e16be57d42bdc003fd601b94e054c7c25ebd290e
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59597097"
---
# <a name="case-study---my-first-year-on-the-hololens-design-team"></a>Étude de cas - équipe de conception de ma première année sur l’HoloLens

Mon parcours à partir d’un flatland 2D pour le monde en 3D démarré lorsque j’ai rejoint l’équipe de conception de HoloLens en janvier 2016. Avant de rejoindre l’équipe, j’ai dû très peu d’expérience dans la conception 3D. Il en retournait le proverbe chinois sur un parcours de miles mille commençant par une seule étape, sauf dans le cas présent, cette première étape a été une année bissextile !

![En prenant l’année bissextile de 2D en 3D](images/2D_to_3D-800px.gif)<br>
*En prenant l’année bissextile de 2D en 3D*

> *« J’ai pensé que j’avais est passé dans le siège du conducteur sans savoir comment piloter la voiture. J’ai été submergé et peur, toutefois, très concentrée. »*<br>
> — HAÉ Jin Lee

L’année dernière, j’ai choisi les compétences et connaissances aussi rapidement que possible, mais j’ai toujours beaucoup à apprendre. Ici, j’ai écrit des 4 observations avec un didacticiel vidéo documenter Ma transition à partir d’un 2D pour le Concepteur d’interactions 3D. J’espère que mon expérience vous incitera les autres concepteurs de l’année bissextile entrent en 3D.

## <a name="good-bye-frame-hello-spatial--diegetic-ui"></a>Image d’un adieu. Hello spatial / diegetic l’interface utilisateur

Chaque fois que j’ai conçu affiches, les magazines, les sites Web ou les écrans de l’application, un cadre défini (généralement un rectangle) a été une constante à chaque problème. Sauf si vous lisez ce billet dans un HoloLens ou un autre périphérique de réalité virtuelle, vous êtes *envisager cela depuis l’extérieur* via l’écran 2D protégée en toute sécurité au sein d’un frame. Le contenu est externe à vous. Toutefois, casque de réalité mixte *élimine le frame*, de sorte que vous êtes dans l’espace de contenu, rechercher et parcourir le contenu à partir de l’intégrale.

J’ai compris ce point de vue conceptuel, mais au début, j’ai commis l’erreur de transfert simplement de pensée 2D dans un espace 3D. Qui évidemment pas fonctionné correctement, car un espace 3D a ses propres propriétés uniques telle qu’une modification de la vue (basé sur le mouvement de la tête de l’utilisateur) et [autre exigence pour le confort de l’utilisateur](https://www.youtube.com/watch?v=-606oZKLa_s/) (basé sur les propriétés de périphériques et les êtres humains à l’aide de les). Par exemple, dans un espace de conception de l’interface utilisateur 2D, le verrouillage des éléments d’interface utilisateur dans le coin d’un écran est un modèle très courant, mais ce style HUD (Head d’affichage) l’interface utilisateur ne vous sentez pas naturel dans les expériences MR/VR ; Il est un obstacle à immersion de l’utilisateur dans l’espace et provoque des maux de l’utilisateur. Cela revient à avoir une particule poussière ennuyeux sur votre LUNETTES qui vous sont morts pour vous débarrasser des. Au fil du temps, j’ai appris qu’il semble plus naturel pour positionner du contenu dans l’espace 3D et ajouter le comportement de verrouillage de corps qui fait le suivi du contenu de l’utilisateur à une distance fixe relative.

![Body-locked](images/bodylockedtagalong.gif)<br>
*Body-locked*

<br>

![Verrouillé-World](images/worldlocked.gif)<br>
*Verrouillé-World*

### <a name="fragments-an-example-of-great-diegetic-ui"></a>Fragments : Un exemple d’excellent Diegetic UI

[Fragments](https://www.microsoft.com/p/fragments/9nblggh5ggm8), un policier TIR crime développé par [Asobo Studio](http://www.asobostudio.com/) pour HoloLens illustre un excellent UI Diegetic. Dans ce jeu, l’utilisateur devient un caractère principal, un détective qui tente de résoudre un mystère. Les indices pivotal pour résoudre cette mystère obtient disséminées dans l’espace physique de l’utilisateur et sont souvent incorporé à l’intérieur d’un objet fictif plutôt qu’existant sur leurs propres. Cette diegetic l’interface utilisateur a tendance à être moins détectables à l’interface utilisateur verrouillé de corps, donc l’équipe Asobo utilisé intelligemment les nombreux signaux, y compris la direction du regard des caractères virtuel, du son, clair et guides (par exemple, la flèche pointant vers l’emplacement de l’indice) pour obtenir l’attention de l’utilisateur.

![Fragments - exemples de Diegetic UI](images/fragments-game-example-1.jpg)<br>
*Fragments - exemples de Diegetic UI*

### <a name="observations-about-diegetic-ui"></a>Observations sur diegetic l’interface utilisateur

Spatiale de l’interface utilisateur (body-verrouillée et verrouillé de world) et de diegetic l’interface utilisateur ont leurs propres forces et les faiblesses. J’encourage les concepteurs pour essayer autant d’applications MR/VR que possible et à développer leur propre présentation et sensibilité pour l’interface utilisateur différentes méthodes de positionnement.

## <a name="the-return-of-skeuomorphism-and-magical-interaction"></a>Le retour de skeuomorphisme et interaction magique

Skeuomorphisme, une interface numérique qui reproduit la forme d’objets du monde réel a été « ne » 5 à 7 ans dans le secteur de la conception. Lors de l’Apple a finalement donné permet de conception plate dans iOS 7, il semblait comme skeuomorphisme, détrompez-vous. enfin comme une méthodologie de conception d’interface. Mais ensuite, un nouveau support casque de MR/VR est arrivé sur le marché et il semble que skeuomorphisme retourné à nouveau. : )

### <a name="job-simulator-an-example-of-skeuomorphic-vr-design"></a>Simulateur de travail : Un exemple de conception VR skeuomorphic

[Simulateur de travail](http://jobsimulatorgame.com/), un jeu saugrenu développé par [Owlchemy Labs](https://owlchemylabs.com/) fait partie de l’exemple plus populaires pour la conception VR skeuomorphic. Dans ce jeu, les lecteurs sont transportés futur où robots remplacement l’homme et humains visitez musée pour découvrir ce que ça ressemble pour effectuer des tâches courantes à un des quatre différents travaux : Automatique garagiste, Chef d’épicerie, Store régisseur ou employé de bureau.

L’avantage de skeuomorphisme est clair. Environnements familiers et des objets dans ce jeu nouvelle VR aider les utilisateurs à se sentent plus à l’aise et présent dans l’espace virtuel. Il les rend également le sentiment qu’ils sont dans le contrôle en associant des connaissances familiers et des comportements avec les objets et leurs réactions physiques correspondantes. Par exemple, pour une tasse de café de boisson, personnes suffit remonter à la machine à café, appuyez sur un bouton, saisissez la poignée cup et incliner vers leur bouche comme ils le feraient dans le monde réel.

![Simulateur de travail](images/job-simulator.gif)<br>
*Simulateur de travail*

MR/VR étant toujours un support de développement, à l’aide d’un certain degré de skeuomorphisme est nécessaire pour démystifier la technologie MR/VR et présenter à un public plus large dans le monde entier. En outre, à l’aide de skeuomorphisme ou représentation réaliste pourrait être intéressant pour des types spécifiques d’applications telles que de simulation de chirurgie ou de vol. Étant donné que l’objectif de ces applications est de développer et affiner les compétences spécifiques qui peuvent être appliqués directement dans le monde réel, la simulation est proche de la réalité, est de la base de connaissances plus transférable.

N’oubliez pas que skeuomorphisme n'est qu’une seule approche. Le potentiel du monde MR/VR est bien supérieur à celle et concepteurs doivent s’efforcer à créer des interactions hyper naturel magiques — nouveau intuitivité qui est possibles de manière unique dans le monde de MR/VR. Comme point de départ, envisagez d’ajouter des compétences magiques à des objets ordinaires pour permettre aux utilisateurs répondre à leurs souhaits fondamentaux, y compris téléportation et omniscience.

![Porte de magique de Doraemon (à gauche) et slippers(right) Ruby](images/doraemons-magical-door-and-ruby-slippers.jpg)<br>
*Porte de magique de Doraemon (à gauche) et slippers(right) ruby*

### <a name="observations-about-skeuomorphism-in-vr"></a>Observations sur skeuomorphisme dans VR

À partir de « N’importe quel endroit de la porte » dans Doraemon, « Ruby chaussons » dans l’Assistant de g à « Mappage de Maurader » dans Harry Potter, exemples d’objets ordinaires avec puissance magique sont nombreux dans fiction populaires. Ces objets magiques nous aider à visualiser une connexion entre le monde réel et le formidable, entre les nouveautés et ce qui pourrait être. N’oubliez pas que lors de la conception magique ou surréalistes un seul objet doit garantir un équilibre entre les fonctionnalités et de divertissement. Méfiez-vous de la tentation de créer quelque chose purement magique uniquement pour des raisons de sécurité de fantaisie.

## <a name="understanding-different-input-methods"></a>Présentation des différentes méthodes d’entrée

Lorsque j’ai conçu pour le support 2D, j’ai dû vous concentrer sur tactile, souris et interactions de clavier pour les entrées. Dans l’espace de conception MR/VR, notre corps devient l’interface et les utilisateurs sont en mesure d’utiliser un choix élargi de méthodes d’entrée : notamment vocale regards, mouvement, [6-DDL contrôleurs](https://en.wikipedia.org/wiki/Six_degrees_of_freedom)et que vous permettre de connexion les plus intuitive et directe avec des objets virtuels.

![Entrées disponibles dans HoloLens](images/inputs.jpg)<br>
*Entrées disponibles dans HoloLens*

> *« Tout est idéal pour quelque chose et les pires pour autre chose ».*<br>
> — [Bill Buxton](https://www.billbuxton.com/)

Par exemple, les mouvements d’entrée à l’aide de la main système et les capteurs de l’appareil photo sur un appareil HMD libère manuellement des utilisateurs à partir de maintenant les contrôleurs ou des gants sweaty, mais une utilisation fréquente peut provoquer la fatigue physique (appelées gorilla arm). En outre, les utilisateurs doivent conserver leurs mains au sein de la ligne de la vue ; Si l’appareil photo ne peut pas voir les mains, entre les mains ne peut pas être utilisés.

La saisie vocale est bonne pour parcourir les tâches complexes, car elle permet aux utilisateurs de couper par le biais des menus imbriqués avec une seule commande (par exemple, « afficher les films effectuées par Laika studio. ») et il est également très économique associée à la modalité d’autres (par exemple, « Me font Face » commande oriente le HOLOGRAMME un utilisateur consulte vers l’utilisateur). Toutefois, la saisie vocale peut ne pas fonctionne correctement dans un environnement bruyant ou ne peut pas appropriée dans un espace très calme.

Outre les gestes et paroles, à main suivies contrôleurs (par exemple, Oculus touch, Vive, etc.) sont des méthodes d’entrée très populaires étant facile à utiliser, précise, exploitez populaire [proprioception](https://en.wikipedia.org/wiki/Proprioception)et fournir des aides HAPTIQUES passifs. Toutefois, ces avantages au détriment de ne pas pouvoir être mains sans système d’exploitation et d’utiliser le suivi du doigt complète.

![Senso (à gauche) et Manus VR(Right)](images/senso-and-manus-vr.jpg)<br>
*Senso (à gauche) et Manus VR (à droite)*

Bien que pas aussi populaire en tant que contrôleurs, gants gagnent à nouveau grâce à la vague MR/VR. Plus récemment, entrée du cerveau/avis ont démarré à susciter en tant qu’interface pour les environnements virtuels en intégrant le capteur CEE ou EMG casque (par exemple, [MindMaze VR](http://www.mindmaze.com/)).

### <a name="observations-about-input-methods"></a>Observations sur les méthodes d’entrée

Il s’agit seulement un échantillon de périphériques d’entrée disponibles sur le marché pour MR/VR. Elles continueront à proliférer jusqu'à ce que l’industrie évolue et s’engage sur les meilleures pratiques. En attendant, les concepteurs doivent rester informés des nouveaux périphériques d’entrée et être familiarisé avec les méthodes d’entrée spécifiques pour leur projet particulier. Pour rechercher des solutions innovantes à l’intérieur des limites, tout en jouant également sur les avantages d’un appareil, les concepteurs ont besoin.

## <a name="sketch-the-scene-and-test-in-the-headset"></a>La scène de croquis et de test dans le casque

Lorsque j’ai travaillé en 2D, j’ai décrit principalement seulement le contenu. Toutefois, dans l’espace de réalité mixte qui n’était pas suffisant. J’ai dû esquissez la scène entière d’imaginer mieux les relations entre l’utilisateur et les objets virtuels. Pour aider à mon raisonnement spatiale, j’ai commencé esquisser des scènes [cinéma 4D](https://www.maxon.net/en/products/cinema-4d/overview/) et créent parfois des ressources simples pour le prototypage dans [Maya](http://www.autodesk.com/products/maya/overview/). J’avais jamais utilisé un programme avant de rejoindre l’équipe de HoloLens et je suis toujours un débutants, mais fonctionne avec ces programmes 3D sans aucun doute m’a aidé à se familiariser avec la nouvelle terminologie, tel que [nuanceur](https://en.wikipedia.org/wiki/Shader) et [IK (inverse cinématique)](https://knowledge.autodesk.com/support/maya/learn-explore/caas/CloudHelp/cloudhelp/2016/ENU/Maya/files/GUID-07C3BA47-32BB-477B-B6C5-1090E5C9B81C-htm.html/).

**« Quel que soit le plus proche j’ai décrit la scène en 3D, l’expérience réelle dans casque était presque jamais le même que l’ébauche de projet. C’est pourquoi il est important de tester la scène dans la cible casques. » — HAÉ Jin Lee**

Pour le prototypage d’HoloLens, j’ai essayé toutes les didacticiels à [Académie de réalité mixte](academy.md) pour démarrer. Puis j’ai commencé à jouer avec [HoloToolkit.Unity](https://github.com/Microsoft/HoloToolkit-Unity/) que Microsoft offre aux développeurs pour accélérer le développement d’applications HOLOGRAPHIQUE. Lorsque je suis bloqué par quelque chose, j’ai publié ma question à [HoloLens Question & réponse Forum](https://forums.hololens.com/categories/questions-and-answers/).

Après avoir acquis une compréhension élémentaire de prototypage de HoloLens, je souhaitais permettre à d’autres non codeurs au prototype sur leurs propres. Par conséquent, j’ai apporté un didacticiel vidéo qui explique comment développer une simple PROJECTILES à l’aide de HoloLens. J’ai expliquer brièvement les concepts de base, par conséquent, même que si vous avez aucune expérience en développement de HoloLens, vous pourrez suivre la procédure.

<br>

>[!VIDEO https://www.youtube.com/embed/58612RT2CT8]
*J’ai fait ce didacticiel simple pour les non programmeurs, comme moi.*

Pour le prototypage VR, j’ai des cours gratuits à [VR Dev School](http://learn.vrdev.school/) et aussi pris [la création de contenu 3D de réalité virtuelle](https://www.lynda.com/Unreal-Engine-tutorials/3D-Content-Creation-Virtual-Reality/482055-2.html?srchtrk=index%3a1%0alinktypeid%3a2%0aq%3aVirtual+Reality+%0apage%3a1%0as%3arelevance%0asa%3atrue%0aproducttypeid%3a2/) sur Lynda.com. VR Dev school fourni que plus connaissances approfondies de codage et le cours Denise m’a proposé une agréable introduction courte pour la création d’éléments multimédias pour VR.

## <a name="take-the-leap"></a>Prendre l’avancée

Un an, j’ai pensé que tout ceci a été insurmontable. Maintenant je peux vous dire qu’il était de 100 % en vaut-il la peine. MR/VR est encore très jeune moyenne et il existe de nombreuses possibilités intéressantes en attente d’être mis en œuvre. Je pense inspiration et chanceux être en mesure de lire une petite partie de la conception de l’avenir. J’espère que vous allez me joindre sur le parcours dans l’espace 3D !

## <a name="about-the-author"></a>À propos de l’auteur

<table style="border-collapse:collapse" padding-left="0px">
<tr>
<td style="border-style: none" width="60"><img alt="Picture of Hae Jin Lee" width="60" height="60" src="images/haejinlee.jpg"></td>
<td style="border-style: none"><b>HAÉ Jin Lee</b><br>Concepteur UX @Microsoft</td>
</tr>
</table>

 
