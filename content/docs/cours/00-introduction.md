---
title: "Chapitre 0 : introduction"
---

# Chapitre 0 : introduction
Unity[^1] est une plateforme de développement 2D / 3D temps-réelle.
Elle permet de créer de nombreuses applications finales, comme par exemple :
1. des cinématiques 3D temps-réelles;
2. des jeux vidéo 2D;
3. des jeux vidéo 3D;
4. des applications de réalité virtuelle, de réalité augmentée et de réalité mixte;
5. des visualisations 3D temps-réelles pour l'architecture et l'industrie.

Des exemples d'applications développées avec Unity sont disponibles dans la playlist suivante :
<center>
<iframe width="734" height="413" src="https://www.youtube.com/embed/videoseries?list=PLoMYgUbrKKtdJFJc0irQnTctVRSXH1-B5" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</center>

Le potentiel de la visualisation 3D temps-réelle en général est très important.
En particulier, une étude de Forrester (avril 2020) commandée par Unity[^2] montre que :
1. sur <strong>348</strong> leaders de l'industrie, <strong>19%</strong> y font déjà appel et parmi ceux-ci, <strong>94%</strong> pensent l'utiliser encore plus dans le futur;
2. <strong>55%</strong> de ces leaders pensent en avoir besoin dans les 2 années à venir;
3. <strong>97%</strong> de ceux qui ne l'utilisent pas encore, pensent que ça modifiera profondément leur façon de produire et de travailler.

## Getting Started
Le ***Unity Hub***[^3] est le point d'entrée pour utiliser Unity.
{{<figure src="images/UnityHub.png#center" width="100%">}}
C'est une application ***standalone*** qui facilite en particulier :
- la gestion de votre compte Unity et des licences associées;
- la création des projets en utilisant des ***templates***;
- la gestion des différentes versions installées de Unity.

Pour créer un nouveau projet, il suffit de choisir le template voulu dans ***Unity Hub*** :
{{<figure src="images/UnityHubCreateProject.png#center" width="100%">}}

Une fois un premier projet créé, l'idéal est de configurer l'intégration avec Visual Studio.
Pour ce faire, il faut aller dans `Edit/Preferences/External Tools/Visual Studio` et modifier les paramètres comme indiqué sur la figure suivante :
{{<figure src="images/UnityVSIntegration.png#center" width="100%">}}

## Ce que nous verrons
Les chapitres de ce cours d'introduction à Unity couvrent les sujets suivants :
- concepts fondamentaux
- caméras
- matériaux
- illumination
- scripting
- animation 3D
- illumination globale
- post-processing
- shaders graph

Le but de chacun de ces chapitres est de présenter une introduction sur chaque sujet et de donner des pistes pour des recherches futures.

## Ce que nous NE verrons PAS
Peut-être encore plus important que ce que nous allons voir, c'est ce que nous ne verrons pas directement.
Certains aspects sont simples et ne posent aucune difficulté pour l'apprentissage autonome.
D'autres sont trop avancées pour être abordés durant ce cours.
Certains enfin sont soit en phase d'abandon, soit toujours en développement.

Les principaux sujets que nous n'aborderons pas sont donc en particulier (liste non-exhaustive) :
- 2D
- multiplayer & réseau
- path finding & IA
- Unity services (Analytics, Collaborate, Cloud build, etc.)
- physique
- et bien plus encore...

{{<hint info >}}
**IMPORTANT**  
À la fin de chaque chapitre, l'étudiant doit comprendre les concepts principaux, les termes spécifiques, et surtout savoir où chercher des informations complémentaires en ligne.
{{</hint >}}

## Slides
{{<slides "https://he-arc.github.io/3292.2-Introduction_Unity-SLIDES/Chap0_Introduction.html">}}


## Références
[^1]: [Unity](https://unity.com/)
[^2]: [How real-time 3D (RT3D) experiences are transforming global industries, Unity](https://blogs.unity3d.com/2020/04/02/how-real-time-3d-rt3d-experiences-are-transforming-global-industries/)
[^3]: [Unity Hub, Unity](https://unity.com/download)
