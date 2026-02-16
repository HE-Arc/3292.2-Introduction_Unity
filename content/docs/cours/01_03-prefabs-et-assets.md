---
title: "Chapitre 1.3 : Prefabs et Assets"
---

# Chapitre 1.3 : Prefabs et Assets
Les ***Prefab*** et les ***Assets*** servent à inclure du contenu dans votre application 3D.

## Prefabs
Un ***Prefab***[^1] peut être vu comme un template de ***GameObject***.
Un ***Prefab*** est donc réutilisable et permet de facilement instancier de multiples copies du même ***GameObject*** dans une scène.
Un des gros avantages des ***Prefabs*** est qu'ils gardent chaque instance synchronisée avec eux-mêmes : tous les changements effectués sur le ***Prefab*** sont automatiquement répercutés sur leurs instances dans la scène.
Conceptuellement, tout ce passe comme ce qui est montré dans l'image suivante :
{{<figure src="images/UnityPrefabs.png#center">}}
Les ***Prefabs*** sont indépendants des scènes et peuvent donc être utilisés pour créer des instances dans plusieurs scènes de l'application.
Pour créer un ***Prefab*** à partir d'un ***GameObject*** dans la scène, il suffit de glisser-déposer ce ***GameObject*** depuis la fenêtre ***Hierarchy*** vers la fenêtre ***Project***.

Les ***Prefabs*** sont identifiables dans la fenêtre ***Hierarchy*** par une icône de cube bleu à gauche de leur nom :
{{<figure src="images/UnityPrefabsInHierarchy.png#center">}}

Pour instancier un ***GameObject*** à partir d'un ***Prefab***, il existe plusieurs méthodes. On peut en particulier le glisser-déposer depuis la fenêtre ***Project*** directement dans la scène ou dans la fenêtre ***Hierarchy***.
Il est aussi possible d'instancier des ***Prefabs*** directement depuis un script.

### Éditer un ***Prefab***
Un ***Prefab*** est modifiable de plusieurs manières.
Lorsqu'un ***Prefab*** est modifié, toutes ses instances sont automatiquement mises à jour.
Il n'est pas possible de changer la structure d'un ***Prefab***, mais on peut lui rajouter des ***GameObjects***.

#### Depuis l’***Inspector***
Il est possible d'éditer un ***Prefab*** depuis la fenêtre ***Inspector*** directement.

#### En mode d'édition de `Prefab` isolé [^2]
Pour passer en mode d'édition de `Prefab` (i.e. `Prefab Mode`) sans la scène (i.e. isolé), il suffit de sélectionner le `Prefab` dans la fenêtre `Project` puis de cliquer sur le bouton `Open Prefab` dans la fenêtre `Inspector`.
Il est aussi possible de double-cliquer sur le `Prefab` dans la fenêtre `Project`.
Unity ouvre ensuite le `Prefab` seul : le fond de la scène change et devient bleu pour indiquer que nous sommes dans un mode spécial.

#### En mode d'édition de `Prefab` avec le contexte [^2]
On passe en mode d'édition de `Prefab` (i.e. `Prefab Mode`) avec la scène (i.e. le contexte), en cliquant sur la flèche à droite de leur nom dans la fenêtre ***Hierarchy***.

La vidéo suivante résume les points mentionnés ci-dessus :
{{< youtube _EFAiUWkN-g >}}

### Instance Overrides
Il est possible de rajouter des variations particulières aux instances d’un ***Prefab***.
On parle alors d'***Instance overrides***[^3].
Les instances modifiées de cette manière restent toujours connectées à leur ***Prefab*** d'origine (i.e. les modifications du ***Prefab*** sont répercutées sur l'instance), à l'exception des paramètres modifiés de l’instance qui ne sont plus mis à jour quand le ***Prefab*** est édité.
Ces ***overrides*** sont indiqués en gras dans l’***Inspector***.

La figure suivante résume succinctement le fonctionnement des ***overrides*** pour les ***Prefabs*** :
{{<figure src="images/UnityPrefabsOverrides.png#center">}}

### Nested Prefabs et Prefabs Variants
Il est possible d'imbriquer des ***Prefabs*** dans des ***Prefabs***.
On appelle ceci des ***Nested Prefabs***[^4].

Des ***overrides*** peuvent aussi être convertis en ***Prefab*** pour créer des ***Prefab Variants***[^5].

En programmation orientée objet, on parlerait de composition pour les ***Nested Prefabs*** et d'héritage pour les ***Prefab Variants***.

Comme nous pouvons le deviner, les ***Prefabs*** offrent une très grande flexibilité.
Cependant, il faut respecter quelques règles pour éviter que les scènes ne deviennent inutilement complexes et finissent par devenir difficilement maintenables.
Ces règles sont très similaires à celles concernant la programmation en générale, à savoir :
- il faut autant que possible rester simple;
- Il est impératif de choisir des noms explicites et adéquats pour les ***GameObjects***, les ***Components*** (ceux que nous créons sous forme de scripts) ainsi que les ***Prefabs***;
- il est fortement recommandé d'éditer les ***Prefabs*** en utilisant le ***Prefab Mode***.

## Assets
Comme rapidement expliqué précédemment, un ***Asset*** représente toute donnée qui est disponible pour le projet.
Ces ***Assets*** peuvent être de différents types[^6] comme des textures, des objets 3D, des sons ou des musiques.
Ils sont soit :
- créés directement dans Unity comme les ***Animation Controller***, les ***Audio Mixers***, etc.;
- créés dans des logiciels externes (comme Blender[^8] par exemple) et importés en tant que fichiers (`.fbx`, `.wav`, `.wav`, etc.);
- ou encore achetés sur l'***Asset Store***[^7] et importés dans le projet.

Les ***Assets*** sont stockés dans le répertoire `Assets` de votre projet.
Unity va ainsi surveiller ce répertoire en permanence et détecter lorsqu'un ***Assets*** est ajouté, enlevé ou modifié.
Par exemple, lorsqu'un fichier contenant un objet 3D est modifié, Unity va automatiquement le réimporter et va mettre votre scène active à jour.
Ceci permet de refléter immédiatement les changements apportés à l'objet 3D.

À chaque ***Assets***, Unity assigne un identifiant unique et lui associe un fichier `.meta` avec le même nom, et dans le même répertoire.
Il faut noter que ces fichier `.meta` sont très importants et ne doivent pas être manipulés.
Enfin, il est possible de modifier la manière dont Unity va importer vos ***Assets*** dans la scène en utilisant les ***Import Settings*** associés.

 ## Pour aller plus loin
<center>
<iframe width="734" height="413" src="https://www.youtube.com/embed/videoseries?list=PLoMYgUbrKKtehxCdlHH1P4lZqJTOdUsbI"
 frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</center>

## Slides
{{<slides "https://he-arc.github.io/3292.2-Introduction_Unity-SLIDES/Chap1_ConceptsFondamentaux.html">}}


## Références
[^1]: [Prefabs, Unity](https://docs.unity3d.com/Manual/Prefabs.html)
[^2]: [Editing a Prefab in Prefab Mode](https://docs.unity3d.com/Manual/EditingInPrefabMode.html)
[^3]: [Instance overrides, Unity](https://docs.unity3d.com/Manual/PrefabInstanceOverrides.html)
[^4]: [Nested Prefabs, Unity](https://docs.unity3d.com/Manual/NestedPrefabs.html)
[^5]: [Prefab Variants, Unity](https://docs.unity3d.com/Manual/PrefabVariants.html)
[^6]: [Common types of assets, Unity](https://docs.unity3d.com/Manual/AssetTypes.html)
[^7]: [Asset Store, Unity](https://assetstore.unity.com)
[^8]: [Blender](https://www.blender.org)
