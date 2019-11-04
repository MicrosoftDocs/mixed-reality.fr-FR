---
title: Étude de cas-ma première année dans l’équipe de conception HoloLens
description: Mon parcours d’un Flatland 2D vers le monde 3D a débuté lorsque j’ai rejoint l’équipe de conception HoloLens en janvier 2016.
author: designnomad
ms.author: haejinl
ms.date: 03/21/2018
ms.topic: article
keywords: Windows Mixed Reality, HoloLens, design, Editorial, Personal
ms.openlocfilehash: 47ed5edd58846687daa4242f7bdbc85dae0f5255
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73436605"
---
# <a name="case-study---my-first-year-on-the-hololens-design-team"></a>Étude de cas-ma première année dans l’équipe de conception HoloLens

Mon parcours d’un Flatland 2D vers le monde 3D a débuté lorsque j’ai rejoint l’équipe de conception HoloLens en janvier 2016. Avant de rejoindre l’équipe, j’avais très peu d’expérience en matière de conception en 3D. Il s’agissait de la proverbe chinoise d’un trajet d’un millier de milliers à partir d’une seule étape, sauf que dans mon cas, la première étape était un bond !

![passer du 2D à la](images/2D_to_3D-800px.gif) 3D<br>
*Passer du 2D à la 3D*

> *«J’ai pensé que j’avais fait passer le siège du conducteur sans savoir comment le conduire. J’étais submergé et effrayé, mais très concentré.»*<br>
> — HAE Jin Lee

Au cours de l’année écoulée, j’ai choisi les compétences et les connaissances aussi rapidement que possible, mais j’ai toujours beaucoup à apprendre. Ici, j’ai écrit 4 observations avec un didacticiel vidéo qui documente ma transition d’un concepteur d’interactions 2D en 3D. J’espère que mon expérience incitera d’autres concepteurs à passer à la 3D.

## <a name="good-bye-frame-hello-spatial--diegetic-ui"></a>Cadre bien adieu. Interface utilisateur spatiale Hello/diegetic

À chaque fois que j’ai conçu des affiches, des magazines, des sites Web ou des écrans d’application, un cadre défini (généralement un rectangle) était une constante pour chaque problème. À moins que vous n’ayez lu cette publication dans un appareil HoloLens ou un autre appareil VR, vous *Regardez cela depuis l’extérieur* jusqu’à l’écran 2D protégé en toute sécurité dans un cadre. Le contenu est externe à vous. Toutefois, le casque de *la réalité mixte élimine le cadre*, de sorte que vous vous trouvez dans l’espace de contenu, en regardant et en parcourant le contenu de l’extérieur.

J’ai compris cela, mais dans le début j’ai fait l’erreur de simplement transférer la pensée 2D dans l’espace 3D. Cela ne fonctionnait évidemment pas correctement, car l’espace 3D a ses propres propriétés uniques, telles que la modification de la vue (en fonction du mouvement de l’utilisateur) et la [nécessité d’un confort d’utilisation différent pour le confort](https://www.youtube.com/watch?v=-606oZKLa_s/) de l’utilisateur (en fonction des propriétés des appareils et des êtres humains). Par exemple, dans un espace de conception d’interface utilisateur 2D, le verrouillage des éléments d’interface utilisateur dans le coin d’un écran est un modèle très courant, mais cette interface de style HUD Cela entrave l’immersion de l’utilisateur dans l’espace et entraîne une gêne de l’utilisateur. C’est comme s’il s’agissait d’une particule de poussière ennuyeux sur vos lunettes, que vous ne vous débarrassez pas. Au fil du temps, j’ai appris qu’il semble plus naturel de positionner le contenu dans l’espace 3D et d’ajouter un comportement verrouillé qui fait en sorte que le contenu suive l’utilisateur à une distance fixe relative.

![](images/bodylockedtagalong.gif) verrouillé<br>
*Corps-verrouillé*

<br>

![](images/worldlocked.gif) verrouillée dans le monde<br>
*Verrouillé par le monde*

### <a name="fragments-an-example-of-great-diegetic-ui"></a>Fragments : exemple d’interface utilisateur de Great Diegetic

Les [fragments](https://www.microsoft.com/p/fragments/9nblggh5ggm8), un crime de criminalité pour la première personne, développé par [Asobo Studio](https://www.asobostudio.com/) pour HoloLens, illustrent une interface utilisateur formidable Diegetic. Dans ce jeu, l’utilisateur devient un caractère principal, un détective qui tente de résoudre un mystère. Les indices dynamiques permettant de résoudre ce mystère se trouvent dans la chambre physique de l’utilisateur et sont souvent incorporés à l’intérieur d’un objet fictif plutôt que d’être existants. Cette interface utilisateur diegetic a tendance à être moins détectable que l’interface utilisateur verrouillée, de sorte que l’équipe Asobo utilise intelligemment de nombreuses indications, y compris les caractères virtuels « direction du point d’arrêt, son, lumière et repères » (par exemple, flèche pointant vers l’emplacement de l’indice) pour attirer l’attention de l’utilisateur.

Fragments de ![-exemples d’interface utilisateur Diegetic](images/fragments-game-example-1.jpg)<br>
*Fragments-exemples d’interface utilisateur Diegetic*

### <a name="observations-about-diegetic-ui"></a>Observations sur l’interface utilisateur diegetic

L’interface utilisateur spatiale (à la fois verrouillée et verrouillée dans le monde) et l’interface utilisateur diegetic ont leurs propres forces et faiblesses. Je encourage les concepteurs à essayer autant d’applications MR/VR que possible, et à développer leurs propres compréhension et Sensibility pour diverses méthodes de positionnement de l’interface utilisateur.

## <a name="the-return-of-skeuomorphism-and-magical-interaction"></a>Retour de skeuomorphisme et de l’interaction magique

Skeuomorphisme, une interface numérique qui imite la forme des objets réels a été « non cool » pour les 5 à 7 dernières années dans le secteur de la conception. Quand Apple a finalement donné la possibilité de concevoir une conception plate dans iOS 7, il semblait que Skeuomorphisme était finalement mort comme une méthodologie de conception d’interface. Mais ensuite, un nouveau casque est arrivé au marché et il semble que Skeuomorphisme retournait. : )

### <a name="job-simulator-an-example-of-skeuomorphic-vr-design"></a>Job Simulator : exemple de conception skeuomorphic VR

[Job Simulator](https://jobsimulatorgame.com/), un jeu saugrenu développé par [Owlchemy Labs](https://owlchemylabs.com/) est l’un des exemples les plus populaires pour la conception de skeuomorphic VR. Au sein de ce jeu, les joueurs sont transportés dans le futur où les robots remplacent les êtres humains et les hommes visitent un musée pour découvrir ce qu’ils estiment qu’ils peuvent effectuer des tâches banales à l’un des quatre travaux suivants : automécanicien, Gourmet chef, Store clerk ou Worker Office.

L’avantage de Skeuomorphisme est clair. Les environnements et les objets familiers au sein de ce jeu permettent aux nouveaux utilisateurs de VR de s’habituer à l’espace virtuel. Cela leur donne également l’impression d’être contrôle en associant des connaissances et des comportements familiers aux objets et aux réactions physiques correspondantes. Par exemple, pour boire une tasse de café, les gens doivent simplement se rendre sur la machine café, appuyer sur un bouton, saisir la poignée de la tasse et l’incliner vers leur bouche comme dans le monde réel.

Simulateur de travail ![](images/job-simulator.gif)<br>
*Simulateur de travail*

Étant donné qu’il s’agit toujours d’un support de développement, l’utilisation d’un certain degré de skeuomorphisme est nécessaire pour déduire la technologie de m/VR et l’introduire dans un public plus large dans le monde entier. En outre, l’utilisation de skeuomorphisme ou d’une représentation réaliste peut être bénéfique pour des types spécifiques d’applications telles que l’intervention chirurgicale ou la simulation de vol. Étant donné que l’objectif de ces applications est de développer et d’affiner des compétences spécifiques qui peuvent être appliquées directement dans le monde réel, plus la simulation est proche du monde réel, plus la connaissance est transmissible.

N’oubliez pas que skeuomorphisme n’est qu’une seule approche. Le potentiel du monde de m/VR est bien plus grand que cela, et les concepteurs doivent s’efforcer de créer des interactions hyper-naturelles magiques, de nouveaux intuitivité qui sont uniques dans le monde de m/VR. Au départ, envisagez d’ajouter des pouvoirs magiques aux objets ordinaires pour permettre aux utilisateurs de s’y conformer, y compris les téléportions et les omniscience.

![porte magique de Doraemon (à gauche) et des glissantes Ruby (à droite)](images/doraemons-magical-door-and-ruby-slippers.jpg)<br>
*Doraemon (à gauche) et des glissants Ruby (à droite)*

### <a name="observations-about-skeuomorphism-in-vr"></a>Observations sur skeuomorphisme en VR

De « portes en tout lieu » dans Doraemon, « Ruby glissants » dans l’Assistant de oz à « carte de Maurader » dans Harry Potter, exemples d’objets ordinaires avec une puissance de magie dans les fictions populaires. Ces objets magiques nous aident à visualiser une connexion entre le monde réel et le fantastique, entre ce qui est et ce qui pourrait être. N’oubliez pas que lors de la conception de l’objet magique ou Surreal, il faut trouver un juste équilibre entre les fonctionnalités et le divertissement. Méfiez-vous de la tentation de créer des choses purement magiques uniquement pour les besoins de la nouveauté.

## <a name="understanding-different-input-methods"></a>Comprendre les différentes méthodes d’entrée

Lorsque j’ai conçu pour le support 2D, j’ai dû me concentrer sur les interactions tactiles, de souris et de clavier pour les entrées. Dans l’espace de conception de m/VR, notre corps devient l’interface et les utilisateurs peuvent utiliser une sélection plus large de méthodes d’entrée : notamment la parole, le point de regard, le mouvement, les [contrôleurs 6-DDL](https://en.wikipedia.org/wiki/Six_degrees_of_freedom)et les gants qui offrent une connexion plus intuitive et directe aux objets virtuels.

![entrées disponibles dans HoloLens](images/inputs.jpg)<br>
*Entrées disponibles dans HoloLens*

> *« Tout est idéal pour un élément, et pire pour un autre. »*<br>
> — [Bill polices Buxton](https://www.billbuxton.com/)

Par exemple, l’entrée de mouvement à l’aide de la main et des capteurs d’appareil photo sur un appareil HMD libère les utilisateurs des contrôleurs ou des gants de transpiration, mais leur utilisation fréquente peut entraîner une fatigue physique (un. k. a Gorilla ARM). En outre, les utilisateurs doivent garder leurs mains dans la ligne de vue ; Si l’appareil photo ne peut pas voir les mains, les mains ne peuvent pas être utilisées.

La saisie vocale est intéressante pour traverser des tâches complexes, car elle permet aux utilisateurs de couper les menus imbriqués à l’aide d’une commande (par exemple, « montrez-moi les films réalisés par Laika Studio ») et également très économique lorsqu’elles sont associées à d’autres modalités (par exemple, la commande « face me » oriente le hologramme qu’un utilisateur examine vers l’utilisateur). Toutefois, l’entrée vocale peut ne pas fonctionner correctement dans un environnement bruyant ou ne pas convenir dans un espace très silencieux.

Outre les gestes et la parole, les contrôleurs suivis par la main (par exemple, Oculus Touch, vive, etc.) sont des méthodes d’entrée très populaires, car ils sont faciles à utiliser, précis, exploitent les [proprioception](https://en.wikipedia.org/wiki/Proprioception)des personnes et fournissent des signaux haptique passifs. Toutefois, ces avantages peuvent s’avérer insuffisants et utiliser le suivi complet des doigts.

![Senso (à gauche) et Manus VR (à droite)](images/senso-and-manus-vr.jpg)<br>
*Senso (à gauche) et Manus VR (à droite)*

Bien qu’ils ne soient pas aussi populaires que les contrôleurs, les gants gagnent à nouveau de la Momentum grâce à la vague de MR/VR. L’entrée la plus récente, le cerveau/l’esprit, a commencé à tirer parti de la traction en tant qu’interface pour les environnements virtuels en intégrant le capteur EEG ou EMG au casque (par exemple, [MINDMAZE VR](https://www.mindmaze.com/)).

### <a name="observations-about-input-methods"></a>Observations sur les méthodes d’entrée

Il s’agit simplement d’un exemple de périphériques d’entrée disponibles sur le marché pour m/VR. Ils continueront de se répandre jusqu’à ce que le secteur vieillise et accepte les meilleures pratiques. Jusqu’à présent, les concepteurs doivent rester informés des nouveaux périphériques d’entrée et être bien entrés dans les méthodes d’entrée spécifiques pour leur projet particulier. Les concepteurs doivent rechercher des solutions créatives à l’intérieur de limitations, tout en lisant également les forces d’un appareil.

## <a name="sketch-the-scene-and-test-in-the-headset"></a>Esquissez la scène et le test dans le casque

Lorsque j’ai travaillé en 2D, je n’ai fait que simplement le contenu. Toutefois, dans un espace de réalité mixte qui n’était pas suffisant. J’ai dû esquisser l’intégralité de la scène pour mieux imaginer les relations entre l’utilisateur et les objets virtuels. Pour aider mon pensée spatiale, j’ai commencé à esquisser des scènes dans [Cinema 4D](https://www.maxon.net/en/products/cinema-4d/overview/) et parfois à créer des ressources simples pour le prototypage dans [Maya](https://www.autodesk.com/products/maya/overview/). Je n’avais jamais utilisé l’un ou l’autre programme avant de rejoindre l’équipe HoloLens et je suis toujours un débutant, mais l’utilisation de ces programmes 3D m’a aidé à se familiariser avec la nouvelle terminologie, telle que le [nuanceur](https://en.wikipedia.org/wiki/Shader) et la [cinématique inverse](https://knowledge.autodesk.com/support/maya/learn-explore/caas/CloudHelp/cloudhelp/2016/ENU/Maya/files/GUID-07C3BA47-32BB-477B-B6C5-1090E5C9B81C-htm.html/).

**«Quel que soit le degré d’esquisse de la scène en 3D, l’expérience réelle du casque n’était presque jamais la même que l’esquisse. C’est pourquoi il est important de tester la scène dans les casques cibles.» — HAE Jin Lee**

Pour le prototypage de HoloLens, j’ai essayé tous les didacticiels des [didacticiels de réalité mixte](tutorials.md) pour commencer. Ensuite, j’ai commencé à jouer avec [HoloToolkit. Unity](https://github.com/Microsoft/HoloToolkit-Unity/) que Microsoft offre aux développeurs pour accélérer le développement d’applications holographiques. Lorsque je me suis bloqué avec un problème, j’ai publié une question sur la [question HoloLens & Forum de réponse](https://forums.hololens.com/categories/questions-and-answers/).

Après avoir acquis une compréhension de base du prototypage HoloLens, je voulais permettre à d’autres non-codeurs de prototyper eux-mêmes. J’ai donc créé un didacticiel vidéo qui explique comment développer un projectile simple à l’aide de HoloLens. J’explique brièvement les concepts de base, donc même si vous n’avez aucune expérience dans le développement HoloLens, vous devez être en mesure de suivre la procédure.

<br>

>[!VIDEO https://www.youtube.com/embed/58612RT2CT8]
*J’ai fait ce didacticiel simple pour les non-programmeurs comme moi.*

Pour le prototypage de VR, j’ai suivi des cours à [VR dev School](https://learn.vrdev.school/) et j’ai également [créé un contenu 3D pour la réalité virtuelle](https://www.lynda.com/Unreal-Engine-tutorials/3D-Content-Creation-Virtual-Reality/482055-2.html?srchtrk=index%3a1%0alinktypeid%3a2%0aq%3aVirtual+Reality+%0apage%3a1%0as%3arelevance%0asa%3atrue%0aproducttypeid%3a2/) sur Lynda.com. VR dev School m’a fourni des connaissances plus approfondies en matière de codage et la formation Denise bourgeois m’a proposé une brève introduction à la création de ressources pour VR.

## <a name="take-the-leap"></a>Prenez le bond

Il y a un an, j’ai pensé que tout cela était un peu lourd. À présent, je peux vous dire qu’il s’agissait de 100% de l’effort. M/VR est toujours très jeune moyen et il y a tellement de possibilités intéressantes en attente. Je suis inspiré et heureux de pouvoir jouer une petite partie de la conception du futur. J’espère que vous participerez au voyage dans l’espace 3D !

## <a name="about-the-author"></a>À propos de l’auteur

<table style="border-collapse:collapse" padding-left="0px">
<tr>
<td style="border-style: none" width="60"><img alt="Picture of Hae Jin Lee" width="60" height="60" src="images/haejinlee.jpg"></td>
<td style="border-style: none"><b>HAE Jin Lee</b><br>@Microsoft du concepteur UX</td>
</tr>
</table>

 
