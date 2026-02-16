---
title: Utiliser Git avec Unity
author: "Benoit Le Callennec"
date: 2020-10-12
tags : [
    "Unity", "VCS"
    ]
---
Il est indispensable d'utiliser un ***Version Control System*** lorsque l'on travaille sur un projet.
En particulier, un ***VCS*** : 
- aide à travailler de manière collaborative;
- facilite la gestion des différentes versions du projet;
- permet de faire des tests en local, sans risquer de casser les versions existantes;
- autorise à revenir à une version précédente.

Unity propose déjà son propre système appelé ***Unity Collaborate***[^1].
Il en existe beaucoup d'autres comme ***Perforce***, ***Subversion***, ***CVS***, etc.

Nous allons nous concentrer sur le ***VCS*** le plus populaire à savoir ***Git***[^2].

Lors de la création du projet Unity et du dépôt git associé, il faut mettre le fichier `.gitignore` à jour.
Pour cela, on peut tout simplement utiliser le site gitignore.io [^3]: 
{{<figure src="images/gitignoreUnity.png#center" width="100%">}}

Il faut placer le fichier `.gitignore` à la racine du projet Unity :
{{<figure src="images/gitignoreUnityPath.png#center" width="30%">}}

De plus, il faut configurer le projet Unity en allant dans le menu `Edit / Project Settings / Version Control / Mode` et sélectionner `Visible Meta Files` :
{{<figure src="images/UnityVCSSettings.png#center" width="100%">}}
Vous trouverez plus d'informations sur les fichiers `.meta` dans la documentation de Unity [^4];

Enfin, il faut aller dans `Edit / Project Settings / Editor`, et pour le paramètre `Asset Serialization`, sélectionner `Force Texte` :
{{<figure src="images/UnityEditorSettings.png#center" width="100%">}}

Il est très compliqué de fusionner des fichiers de scènes et de Prefabs.
Il est donc important d'éviter les `merge conflicts` pour ces fichiers.
Pour ce faire, il est conseillé :
- d'utiliser différentes scènes;
- d'utiliser les Prefabs autant que possible;
- d'utiliser les `ScriptableObjects`;
- et fréquemment faire des commits.

Enfin, un projet Unity va régulièrement contenir de gros fichiers de données (.wav, .fbx, textures, etc.). 
Il est donc fortement recommandé d'utiliser `git lfs` [^5].

## À regarder (pour aller plus loin)
<center>
<iframe width="734" height="413" src="https://www.youtube.com/embed/videoseries?list=PLoMYgUbrKKtdUaGQO0w8MM3EZh3SYT-fA"
frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</center>

## Références
[^1]: [Unity Collaborate, Unity](https://unity.com/unity/features/collaborate)
[^2]: [Git](https://git-scm.com/)
[^3]: [gitignore for Unity, gitignore.io](https://www.toptal.com/developers/gitignore/api/unity)
[^4]: [Asset Metadata, Unity](https://docs.unity3d.com/Manual/AssetMetadata.html)
[^5]: [Git LFS, GitHub](https://git-scm.com)
