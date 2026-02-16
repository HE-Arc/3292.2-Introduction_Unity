---
title: Erreur de résolution de template de projet
author: "Benoit Le Callennec"
date: 2020-10-08
tags : [
    "Unity", 
    ]
---
Lors de la création d'un nouveau projet, Unity affiche parfois l'erreur "***Failed to resolve project template***" comme indiqué sur la capture suivante :
{{<figure src="images/UnityFailedToResolveProjectTemplate.png#center" width=100% >}}

Ceci est vraisemblablement causé par un bug [^1] lorsque le path est trop long, ou contient des espaces.
Il suffit donc de changer le nom du projet, du répertoire parent, ou de déplacer le projet.

## Références
[^1]: [Failed to resolve project template: Failed to decompress, Forums Unity](https://forum.unity.com/threads/failed-to-resolve-project-template-failed-to-decompress.663214/)