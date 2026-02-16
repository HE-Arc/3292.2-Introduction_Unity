---
title: "Chapitre 7 : Shader Graph"
---

# Chapitre 7 : Shader Graph

{{<hint warning >}}
**IMPORTANT**  
Le {{<unity_keyword `Shader Graph` >}} est compatible avec le {{<unity_keyword `Universal Render Pipeline` >}} et le {{<unity_keyword `High-Definition Render Pipeline` >}}.
Il n'est compatible avec le {{<unity_keyword `Built-in Render Pipeline` >}} que depuis la version 2021.2.
{{</hint >}}

Dans une application 3D, il est primordial de modifier le rendu visuel final de certains objets.
Ceci se fait en écrivant des {{<unity_keyword `Shaders` >}}.
Pour cela, Unity propose un langage spécifique qui s'appelle {{<unity_keyword `ShaderLab` >}}.
{{<unity_keyword `ShaderLab` >}} permet en particulier de facilement et rapidement déclarer des aspects importants de nos {{<unity_keyword `Shaders` >}} comme les passes de rendu, certaines configurations ou la gestion de la transparence.
Le corps des shaders est lui écrit en  {{<unity_keyword `HLSL` >}} (pour High-Level Shader Language)[^HLSL].

De plus, Unity propose un outil qui s'appelle le {{<unity_keyword `Shader Graph` >}}[^UnityShaderGraph].
Le {{<unity_keyword `Shader Graph` >}} permet de créer des {{<unity_keyword `Shaders` >}} de manière visuelle.
Les opérations sont représentées par des {{<unity_keyword `Nodes` >}}, les données en entrée par des {{<unity_keyword `Input Ports` >}}, et les données en sortie par des {{<unity_keyword `Output Ports` >}}.
Pour définir comment les données transitent d'un {{<unity_keyword `Node` >}} vers les autres, les {{<unity_keyword `Ports` >}} sont connectées entre eux.
Enfin, un {{<unity_keyword `Shader` >}} dans le {{<unity_keyword `Shader Graph` >}} peut être paramétré par des {{<unity_keyword `Properties` >}}.
Ces {{<unity_keyword `Properties` >}} sont visibles et éditables directement dans la fenêtre {{<unity_window `Inspector` >}} de l'éditeur.
{{<figure src="images/UnityShaderGraphExample.gif#center" >}}

Un {{<unity_keyword `Shader` >}} créé avec le {{<unity_keyword `Shader Graph` >}} est un {{<unity_keyword `Asset` >}}.
Il faut donc le créer directement dans la fenêtre {{<unity_window `Project` >}} ou dans le menu {{<unity_menu `Asset` >}}.
Ensuite, il faut aller dans le menu {{<unity_menu `Create > Shader` >}} puis choisir le type de {{<unity_keyword `Shader` >}} que nous souhaitons créer.
{{<figure src="images/UnityCreateShaderGraph.png#center" >}}

Une fois créé, nous pouvons ouvrir notre {{<unity_keyword `Shader` >}} directement dans le {{<unity_keyword `Shader Graph` >}} en double-cliquant dessus.
La fenêtre suivante apparaît :
{{<figure src="images/UnityShaderGraphWindow.png#center" >}}

Nous pouvons noter les éléments suivants :

1. la fenêtre {{<unity_window `Blackboard` >}} qui contient la liste des {{<unity_keyword `Properties` >}} du {{<unity_keyword `Shader` >}}, c'est-à-dire l'ensemble des paramètres du {{<unity_keyword `Shader` >}} qui seront modifiables directement depuis l'éditeur.
Pour le moment, elle est vide;
2. la fenêtre {{<unity_window `Graph Inspector` >}} : elle fonctionne de la même manière que la fenêtre {{<unity_window `Inspector` >}} que nous avons déjà utilisée dans l'éditeur.
En particulier, elle affiche les informations importantes concernant les éléments actuellement sélectionnés dans le graph;
3. le {{<unity_keyword `Shader` >}} représenté par un graphe.
Pour le moment, il ne contient que la {{<unity_keyword `Master Stack` >}}.
La {{<unity_keyword `Master Stack` >}} contient en fait le {{<unity_keyword `Vertex Shader` >}} et le {{<unity_keyword `Fragment Shader` >}}.
Ils représentent les sorties effectives de notre {{<unity_keyword `Shader` >}}.
4. le {{<unity_keyword `Main Preview` >}} qui permet de voir directement un aperçu des résultats produits par notre {{<unity_keyword `Shader` >}}.

{{<hint warning >}}
**ATTENTION**

L'emplacement ainsi que la visibilité des fenêtres peuvent varier.
{{</hint >}}

Pour le moment, notre {{<unity_keyword `Shader` >}} ne fait pas grand chose.
Nous allons donc rajouter des {{<unity_keyword `Nodes` >}}, puis établir les connexions nécessaires entre leurs {{<unity_keyword `Ports` >}} respectifs.
Pour créer un nouveau {{<unity_keyword `Node` >}}, il suffit de faire un clic droit puis de sélectionner unity {{<unity_menu `Create Node` >}} :
{{<figure src="images/UnityShaderGraphCreateNewNode.png#center" >}}

La fenêtre qui apparaît vous affiche la liste de tous les {{<unity_keyword `Nodes` >}} actuellement disponibles pour le {{<unity_keyword `Shader Graph` >}}.
{{<figure src="images/UnityShaderGraphCreateNewNodeWindow.png#center" >}}

Il en existe déjà beaucoup et chaque nouvelle version de Unity en intègre de nouveaux.
Pour connecter des {{<unity_keyword `Ports` >}} entre eux, il suffit de sélectionner l'{{<unity_keyword `Output Port` >}} du {{<unity_keyword `Node` >}} de départ, et le glisser-déposer sur l'{{<unity_keyword `Input Port` >}} du {{<unity_keyword `Node` >}} d'arrivée.

Par exemple, on peut :
1. créer un {{<unity_keyword `Node` >}} de type {{<unity_keyword `Voronoi` >}};
2. créer un {{<unity_keyword `Node` >}} de type {{<unity_keyword `Color` >}};
3. multiplier leurs sorties avec un {{<unity_keyword `Node` >}} de type ***Multiply*** et connecter son {{<unity_keyword `Output Port` >}} à l'{{<unity_keyword `Input Port` >}} ***Base Color*** du {{<unity_keyword `Fragment Shader` >}};
4. Enfin, on peut faire varier l'{{<unity_keyword `Input Port` >}} ***Angle Offset*** du {{<unity_keyword `Node` >}} {{<unity_keyword `Voronoi` >}} grâce à un {{<unity_keyword `Node` >}} de type ***Time***.

Une fois ces étapes effectuées, on obtient le {{<unity_keyword `Shader Graph` >}} suivant :
{{<figure src="images/UnityShaderGraphVoronoiExample.gif#center" >}}

Pour tester le résultat dans notre scène, il nous faut enfin :
1. enregistrer l'{{<unity_keyword `Asset` >}} en cliquant sur le bouton {{<unity_button `Save Asset` >}} dans la barre d'outils;
2. créer un nouveau {{<unity_keyword `Material` >}} et lui assigner le {{<unity_keyword `Shader` >}} créé;
3. créer un object et lui affecter le {{<unity_keyword `Material` >}}.

Au final, nous obtenons un résultat similaire à ce qui suit :
{{<figure src="images/UnityShaderGraphVoronoiResultsInterm.gif#center" >}}

{{<hint warning >}}
**IMPORTANT** 
Il ne faut pas oublier de sauvegarder son {{<unity_keyword `Shader` >}} en cliquant sur le bouton {{<unity_button `Save asset` >}} pour voir le résultat dans l'éditeur.
{{</hint >}}

Nous avons donc pour le moment créé un {{<unity_keyword `Shader` >}} qui permet de modifier l'aspect des objects auxquels il est attaché.
Cependant, il n'est pas vraiment flexible.
En particulier, nous aimerions pouvoir modifier la couleur finale, ainsi que la vitesse d'animation de notre {{<unity_keyword `Shader` >}}.
Pour ce faire, nous pouvons créer des {{<unity_keyword `Properties` >}}.
Ces {{<unity_keyword `Properties` >}} seront ensuite modifiables depuis l'éditeur, on directement dans un script.
Pour cela, nous devons soit :

- créer de nouvelles {{<unity_keyword `Properties` >}} dans la fenêtre {{<unity_window `Blackboard` >}} en cliquant sur le bouton {{<unity_button `+` >}} et en choisissant le type de {{<unity_keyword `Property` >}} désiré;
- convertir un {{<unity_keyword `Node` >}} de type {{<unity_keyword `Input` >}} existant dans le {{<unity_keyword `Shader Graph` >}}.

En convertissant le {{<unity_keyword `Node` >}} de type {{<unity_keyword `Color` >}}, en rajoutant les {{<unity_keyword `Properties` >}} ***speed*** et ***density*** de type {{<unity_keyword `Float` >}}, et en ajustant les connexions existantes, on obtient le {{<unity_keyword `Shader Graph` >}} suivant :
{{<figure src="images/UnityShaderGraphVoronoiExample2.gif#center" >}}

Maintenant, nous pouvons voir le résultat dans la scène Unity directement et surtout, nous pouvons modifier les {{<unity_keyword `Properties` >}} pour produire des effets variés :
{{<figure src="images/UnityShaderGraphVoronoiExampleInEditor.gif#center" >}}

{{<hint info >}}
**INFORMATIONS**

Pour les {{<unity_keyword `Properties` >}} de type {{<unity_keyword `Float` >}}, on peut spécifier de les afficher avec des {{<unity_keyword `Sliders` >}} en modifiant leurs paramètres dans la fenêtre {{<unity_window `Graph Inspector` >}}.
{{</hint >}}

La couleur en entrée peut enfin être remplacée par une texture.
Dans ce cas, il faut tout simplement créer une {{<unity_keyword `Property` >}} de type {{<unity_keyword `Texture2D` >}}.
Ensuite, il faut créer un {{<unity_keyword `Node` >}} de type {{<unity_keyword `Sample Texture 2D` >}} qui va être en charge d'échantillonner la texture et de retourner les bonnes couleurs, en fonction des UV passées en entrée.

{{<hint danger >}}
**EXERCICE**

Rajouter la possibilité d'utiliser une texture en entrée de notre {{<unity_keyword `Shader Graph` >}}.
{{</hint >}}

## Slides

{{<slides "http://enseignement.pages.ing.he-arc.ch/isc/cours/niveau-3/3292.2-infographie-unity/slides/Chap7_ShaderGraph.html">}}

## Références

[^UnityShaderGraph]: [Shader Graph, Unity](https://docs.unity3d.com/Packages/com.unity.shadergraph@latest/index.html)
[^HLSL]: [High-level shader language (HLSL), Microsoft](https://docs.microsoft.com/en-us/windows/win32/direct3dhlsl/dx-graphics-hlsl)
