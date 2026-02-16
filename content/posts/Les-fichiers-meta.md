---
title: Les fichiers .meta
author: "Benoit Le Callennec"
date: 2022-04-01
tags : [
    "Unity", "VCS"
    ]
---

Comme précisé dans l'article intitulé [Utiliser Git avec Unity](/posts/utiliser-git-avec_unity) : 
> il est indispensable d'utiliser un ***Version Control System*** lorsque l'on travaille sur un projet en Unity.

On remarque cependant que certains fichiers générés doivent tout de même être versionnés, en particulier les fichier **`.meta`**[^AssetMetadata].
Ceci est contre intuitif et semble aller à l'encontre de la philosophie de Git.

Les fichiers `.meta` servent en fait à stocker des metadonnées concernant les {{<unity_keyword `Assets` >}} importés dans les projets.
En particulier, si on sélectionne un {{<unity_keyword `Asset` >}} dans la fenêtre {{<unity_window `Project` >}}, on obtient une fenêtre {{<unity_window `Inspector` >}} qui ressemble à ça :
{{<figure src="images/UnityAssetImportSettings.png#center" width="100%">}}

Tous ces paramètres permettent à Unity de savoir comment importer le fichier correspondant.
Ces informations sont stockées dans le fichier **`.meta`** associé.

Les fichiers **`.meta`** stockent beaucoup d'autres informations.
Pour le vérifier, il suffit d'en ouvrir un dans un éditeur de texte classique :
{{<figure src="images/UnityMetaFileContent.png#center" width="100%">}}

Pour plus d'informations, la documentation de Unity[^AssetMetadata] détaille le fonctionnement interne de ces fichiers **`.meta`**, ainsi que certaines limitations.

## Références
[^AssetMetadata]: [Asset Metadata, Unity](https://docs.unity3d.com/Manual/AssetMetadata.html)