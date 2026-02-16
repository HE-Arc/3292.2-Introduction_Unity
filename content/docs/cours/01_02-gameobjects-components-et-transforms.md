---
title: "Chapitre 1.2 : GameObjects, Components et Transforms"
---

# Chapitre 1.2 : GameObjects, Components et Transforms
Dans ce chapitre, nous allons succinctement voir les éléments fondamentaux qui constituent une scène dans Unity, à savoir les {{<unity_keyword `GameObjects`>}}, les {{<unity_keyword `Components`>}} et les {{<unity_keyword `Transforms`>}}.

## GameObjects
Tout objet dans une application Unity est un {{<unity_keyword `GameObject`>}}[^1], comme par exemple un {{<unity_keyword `Mesh`>}}, une {{<unity_keyword `Camera`>}} ou une {{<unity_keyword `Light`>}}.
{{<figure src="images/UnityGO.png#center" width="100%">}}
  
Cependant, ils n'offrent aucune fonctionnalité à proprement parler.
En effet, les {{<unity_keyword `GameObjects`>}} ne sont en fait que des {{<unity_keyword `Containers`>}} pour des {{<unity_keyword `Components`>}}.
Il est important de noter que tout {{<unity_keyword `GameObject`>}} doit pouvoir être positionné dans la scène.
Ainsi, ils contiennent tous au moins un {{<unity_keyword `Component`>}} de type {{<unity_keyword `Transform`>}}.
En particulier, un {{<unity_keyword `Empty`>}}, qui représente donc un {{<unity_keyword `GameObject`>}} vide, contient un {{<unity_keyword `Component`>}} de type {{<unity_keyword `Transform`>}}.

En allant dans le menu `GameObject / Create Empty`, le {{<unity_keyword `GameObject`>}} ainsi créé ressemble à ce qui suit dans l'{{<unity_keyword `Inspector`>}} :
{{<figure src="images/UnityEmptyGO.png#center">}}

Un {{<unity_keyword `GameObject`>}} est donc formé de la façon suivante :
{{<figure src="images/UnityGameObject.png#center">}}
1. la zone contenant les paramètres relatifs au {{<unity_keyword `GameObject`>}} en lui-même;
2. le {{<unity_keyword `Transform`>}} attaché à tout {{<unity_keyword `GameObject`>}};
3. le ou les {{<unity_keyword `Components`>}} représentant les véritables fonctionnalités du {{<unity_keyword `GameObject`>}};
4. Enfin, durant le développement d'un projet, il est très souvent utile de pouvoir rapidement désactiver des {{<unity_keyword `Components`>}} ou même des {{<unity_keyword `GameObjects`>}}. Ceci peut se faire simplement depuis l'{{<unity_keyword `Inspector`>}} en les activant ou les désactivant.

### Layers
Les {{<unity_keyword `Layers`>}} permettent de grouper des {{<unity_keyword `GameObjects`>}} selon des critères spécifiques.
Par exemple, on peut regrouper tous les {{<unity_keyword `GameObjects`>}} qui représentent des ennemis dans un {{<unity_keyword `Layer`>}} nommé `Enemies`.
On peut aussi filtrer les {{<unity_keyword `GameObjects`>}} affichés dans la scène en fonction de leur {{<unity_keyword `Layer`>}}.
Pour créer un layer, il faut aller dans le menu {{<unity_menu `Edit / Project Settings / Tags and Layers` >}} et ajouter un nouveau {{<unity_keyword `Layer`>}}.
Ensuite, il suffit de sélectionner un {{<unity_keyword `GameObject`>}} et de lui attribuer le {{<unity_keyword `Layer`>}} voulu dans l'{{<unity_keyword `Inspector`>}}.

## Components
Comme dit précédemment, les véritables fonctionnalités d'un {{<unity_keyword `GameObject`>}} sont données par les {{<unity_keyword `Components`>}}[^2] qui lui sont associés.
Pour ajouter un {{<unity_keyword `Component`>}} à un {{<unity_keyword `GameObject`>}}[^3], il faut aller dans le menu `Component` et choisir le {{<unity_keyword `Component`>}} désiré.
Par exemple, pour pouvoir contrôler un {{<unity_keyword `GameObject`>}} avec de la physique, il faut lui rajouter le {{<unity_keyword `Component`>}} {{<unity_keyword `RigidBody`>}} dans le menu `Components / Physics / Rigidbody` :
{{<figure src="images/UnityAddRigidBodyComponent.png#center">}}

On peut aussi rajouter un {{<unity_keyword `Component`>}} à un {{<unity_keyword `GameObject`>}} directement depuis l'{{<unity_keyword `Inspector`>}} en cliquant sur le bouton `Add Component` :
{{<figure src="images/UnityAddRigidBodyComponentWithInspector.png#center">}}
Il suffit alors de rechercher le nom du {{<unity_keyword `Component`>}} que l'on souhaite rajouter, et Unity nous affiche automatiquement ceux disponibles.

Il est intéressant de noter que si l'on crée un {{<unity_keyword `Empty`>}}, et qu'on lui rajoute un {{<unity_keyword `Component`>}} de type {{<unity_keyword `Light`>}}, alors Unity le considère comme une {{<unity_keyword `Light`>}} à part entière et affiche le gizmo associé :
{{<youtube y8IAqyDnCCE >}}

## Transforms
Le {{<unity_keyword `Transform`>}} [^4] est certainement le {{<unity_keyword `Component`>}} le plus important pour un {{<unity_keyword `GameObject`>}}.
Il permet de définir tous les paramètres de transformation du {{<unity_keyword `GameObject`>}} comme sa position, son orientation et ses échelles.
Ce {{<unity_keyword `Component`>}} est tellement important qu'il n'est pas possible de le supprimer d'un {{<unity_keyword `GameObject`>}}.
Les gizmos permettent de modifier un {{<unity_keyword `Transform`>}} simplement et rapidement :
{{<figure src="images/UnityTransformGizmos.png#center">}}

Les {{<unity_keyword `Transforms`>}} peuvent être imbriqués les uns dans les autres : on parle de {{<unity_keyword `Parenting`>}} ou de relation {{<unity_keyword `Parent-Child`>}}.
Toute transformation contenue par à un {{<unity_keyword `Transform`>}} est automatiquement appliquée à tous ces enfants ({{<unity_keyword `Children`>}}).
La vidéo suivante montre comment modifier un {{<unity_keyword `Transform`>}}, comment les parenter, et comment les séparer :
{{< youtube sgLUcdypgy4 >}}

## Slides
{{<slides "http://enseignement.pages.ing.he-arc.ch/isc/cours/niveau-3/3292.2-infographie-unity/slides/Chap1_ConceptsFondamentaux.html">}}

## Références
[^1]: [GameObjects, Unity](https://docs.unity3d.com/Manual/GameObjects.html)
[^2]: [Introduction to components, Unity](https://docs.unity3d.com/Manual/Components.html)
[^3]: [Using Components, Unity](https://docs.unity3d.com/Manual/UsingComponents.html)
[^4]: [Transforms, Unity](https://docs.unity3d.com/Manual/class-Transform.html)
