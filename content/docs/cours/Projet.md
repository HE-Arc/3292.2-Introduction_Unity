---
title: "Projet"
---

# Projet

## Informations Générales
Le projet a pour objectif de réaliser une reproduction 3D de la HE-Arc en utilisant Unity URP.
Il se déroulera par groupe de 2 ou 3 étudiants.
L'exécutable final doit être fonctionnel sur Windows.

Le but est de démontrer que vous connaissez les bases de Unity en intégrant plusieurs notions de manière pertinente dans un projet global.
En particulier, il faudra intégrer les objets 3D réalisés sous Blender lors du semestre d'automne.

Votre projet doit intégrer une majorité des points importants introduits en cours :
- Prefab
- Viewport Rect : pour les Multi-view par exemple
- Depth + Culling Mask : pour mettre l'accent sur des objets particuliers et les afficher par dessus tous les autres éléments de la scène.
Ou pour créer une mini-map par exemple.
- Target Texture : pour créer des écrans de contrôle ou des miroirs par exemple
- Light temps-réelles
- Skybox + ambient + fog
- Ombres
- Lightmaps
- Ambient occlusion
- Coroutines
- Matériaux
- Shadergraph
- Animation 3D
- Blend Trees
- Triggers
- Post-processing

Il est aussi possible d'utiliser d'autres concepts non-vus en cours comme la simulation physique, le path planning ou autres.
Il en sera tenu compte lors de l'évaluation finale du projet.

## Mise en place
Le repo principal GitLab se trouve ici : [https://gitlab-etu.ing.he-arc.ch/isc/2024-25/niveau-3/3292.2-infographie-unity-il/3292_main](https://gitlab-etu.ing.he-arc.ch/isc/2024-25/niveau-3/3292.2-infographie-unity-il/3292_main)
Il faut dans un premier temps le cloner en local.
Ensuite, vous devez cloner votre propre repo dans le répertoire **`Assets/_ROOMS`**.

## Développement
Avant tout, il faut lire la page expliquant comment [Utiliser Git avec Unity](/posts/utiliser-git-avec_unity).

En particulier, toute la salle dont vous êtes responsable doit être contenue dans un Prefab.
Ce Prefab sera intégré dans la scène principale par les professeurs.
Vous êtes libres de faire toutes les modifications nécessaires dans votre propre repo.

Le répertoire **`Main`** contient les Assets principaux.

### À RENDRE
- **Repo git propre :** il faut pouvoir faire git clone et lancer l'application depuis Unity.
- **Rapport :** il faut expliquer quoi regarder succinctement. Quelques pages suffisent.
- **Vidéo de démo (avec voix-off et crédits) :** il faut démontrer les principales fonctionnalités de votre projet (2 minutes maximum).
- **Une démo jouable :** on double-clique, on joue.
