---
title: Erreur de chargement de projets
author: "Benoit Le Callennec"
date: 2020-09-17
tags : [
    "Unity", 
    ]
draft: true
---
Il arrive parfois que lors du chargement de projets nouvellement créés, Unity affiche l'erreur "***Failed to load window layout***" comme indiqué sur la capture suivante :
{{<figure src="images/UnityFailedToLoadWindowLayout.png#center" width=100% >}}

Ceci est vraisemblablement causé par un bug lors de la génération du fichier ***CurrentLayout-default.dwlt*** qui se trouve dans le répertoire ***Library*** de votre projet Unity.
L'idée est donc de laisser Unity en regénérer un correct en appuyant sur le bouton "***Load Default Layout***".
Cependant, même en faisant ça, l'erreur persiste et Unity nous force à quitter.
En quittant, Unity restaure l'ancienne version (incorrecte) du fichier.
L'idée est donc de sauvegarder la version correcte du fichier quelque part, de quitter Unity, puis de la restaurer "à la main", avant de relancer Unity.