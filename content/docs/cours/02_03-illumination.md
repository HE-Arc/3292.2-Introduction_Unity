---
title: "Chapitre 2.3 : illumination"
---

# Chapitre 2.3 : illumination
Afin de voir une scène 3D et les objets qui la composent, il faut rajouter des lumières et les effets associés (ombres, brouillard, réflexions, etc).

Il existe 3 classes de lumières :
- **temps-réelles :** elles sont calculées à l'exécution par Unity. Par conséquent, elles utilisent des techniques peu gourmandes en calculs.
Ces lumières sont appropriées lorsque les objets de la scène sont dynamiques (changent à l'exécution);
- **pré-calculées :** on parle de {{<unity_keyword `Baked Lights` >}}.
Ici, l'illumination est calculée avant l'exécution.
Les résultats sont dans un premier stockés dans des {{<unity_keyword `Lightmaps` >}}, puis réutilisés en temps-réel.
Les techniques utilisées sont plus complexes mais donnent des résultats plus réalistes.
Ces lumières sont appropriées pour des scènes statiques c'est-à-dire qui ne changent pas à l'exécution;
- **hybrides :** enfin, il est possible de mélanger les 2 types de lumières selon les objets 3D considérés.

Ce chapitre se focalise uniquement sur les lumières temps-réelles.
Les techniques plus avancées permettant de faire des rendus photoréalistes seront abordées dans le chapitre dédié à l'[illumination globale](../05-illumination-globale).

## Light Component
Dans Unity, les {{<unity_keyword `Lights` >}}[^1] sont composées et représentées de la manière suivante :
{{<figure src="images/UnityLight.png#center" >}}
En particulier, on remarque :
- le {{<unity_keyword `Gizmo` >}} de la {{<unity_keyword `Light` >}} et son icône associée dans la scène 3D;
- le {{<unity_keyword `Light Component` >}} avec les paramètres des lumières.

Il faut noter qu'une {{<unity_keyword `Light` >}} est un {{<unity_keyword `GameObject` >}}, et donc contient aussi un {{<unity_keyword `Transform` >}}.

Pour créer une {{<unity_keyword `Light` >}}, il faut aller dans le menu {{<unity_menu `GameObject > Light` >}} et choisir le type de lumière désiré, comme indiqué sur la figure suivante :
{{<figure src="images/UnityCreateLight.png#center" >}}
Les {{<unity_keyword `Lights` >}} peuvent être de 4 types :
- ***Directional :*** ici, seule l'orientation est importante;
- ***Point :*** pour ce type de lumières, seule la position a une incidence sur l'illumination;
- ***Spot :*** dans ce cas, modifier la position ou l'orientation de la lumière modifie aussi l'illumination;
- ***Area :*** ce type de lumières est particulier car c'est toute la surface qui a son importance. Ces lumières sont plus complexes à calculer et sont forcément ***Baked*** et non ***Realtime***.

Les principaux paramètres des {{<unity_keyword `Lights` >}} sont modifiables facilement grâce au {{<unity_keyword `Light Explorer` >}} atteignable par le menu {{<unity_menu `Window > Rendering > Light Explorer` >}}.
La figure suivante en donne un aperçu :
{{<figure src="images/UnityLightExplorer.png#center" >}}

### Culling Mask
De manière similaire aux {{<unity_keyword `Cameras` >}}, le paramètre {{<unity_keyword `Culling Mask` >}} permet de spécifier quels groupes d'objets 3D doivent être considérés (rendus) par la {{<unity_keyword `Light` >}}.
{{<figure src="images/UnityLightCullingMask.png#center">}}

Les figures suivantes montrent la différence entre une lumière qui considère tous les objets 3D de la scène, et une lumière que ne considèrent qu'un sous-ensemble de ces objets.
{{< columns >}}
**Tous les objets 3D**
{{<figure src="images/UnityLightCullingMaskWith.png#center" >}}
<--->
**Seulement les objets 3D sélectionnés**
{{<figure src="images/UnityLightCullingMaskWithout.png#center" >}}
{{< /columns >}}

## Lumière environnementale
En plus des {{<unity_keyword `Light Components` >}}, l'environnement participe aussi à l'illumination et a un impact sur l'aspect final de la scène 3D.
La fenêtre de configuration pour les différents paramètres de lumière environnementale est appelée la {{<unity_keyword `Lighting window` >}}[^2] et est accessible dans le menu {{<unity_menu `Window > Rendering > Lighting` >}} comme indiqué sur la figure suivante :
{{<figure src="images/UnityLightingWindowMenu.png#center" >}}

On obtient alors une fenêtre contenant les onglets {{<unity_keyword `Scene` >}}, {{<unity_keyword `Environment` >}} et {{<unity_keyword `Baked Lightmaps` >}}.
En sélectionnant l'onglet {{<unity_keyword `Environment` >}}, la fenêtre affiche quelque chose de similaire à ce qui suit :
{{<figure src="images/UnityLightingWindow.png#center" >}}
Il y a en particulier plusieurs sections que nous détaillons dans la suite :
1. les {{<unity_keyword `Skybox` >}};
2. La lumière ambiante;
3. les réflexions associées à l'environnement;
4. et le brouillard dans la scène 3D.

Les sous-sections suivantes introduisent ces notions à l'exception des réflexions qui sont, quant à elles, abordées dans un chapitre dédié.

### Skybox
Une {{<unity_keyword `Skybox` >}} représente ce qui est visible à l'arrière-plan, quand il n'y a aucun objet 3D pour obstruer la vue.

{{<hint warning >}}
**URP vs HDRP**  
Le système de {{<unity_keyword `Skybox` >}} est différent selon qu'on utilise URP ou HDRP.
Dans ce cours, nous nous focalisons sur URP.
{{</hint >}}

Dans Unity, une {{<unity_keyword `Skybox` >}} est en fait un {{<unity_keyword `Material` >}} avec un {{<unity_keyword `Shader` >}} de type {{<unity_keyword `Skybox` >}}.
Une fois créée, cette {{<unity_keyword `Skybox` >}} peut être soit globale (donc partagée par tous les objets), ou locale pour chaque caméra.
Si elle est globale, alors on peut rajouter le {{<unity_keyword `Material` >}} dans le paramètre {{<unity_keyword `Skybox Material` >}} de la fenêtre {{<unity_keyword `Lighting window` >}}.
Si elle est locale à une caméra, alors il faut dans un premier temps rajouter un {{<unity_keyword `Component` >}} de type {{<unity_keyword `Skybox` >}} à la caméra, puis y associer la {{<unity_keyword `Skybox` >}}.

### Lumière ambiante
La lumière ambiante ({{<unity_keyword `Ambient Light` >}}) est une lumière diffuse, qui vient de toutes les directions à la fois.
Elle est très utile car Les techniques de rendus actuelles "perdent" en général un peu de lumière par rapport à la réalité.
La lumière ambiante est donc une technique simple pour "rehausser" artificiellement le niveau de lumière dans la scène.
Cette lumière permet aussi de rajouter des ambiances particulières en fonction de la teinte utilisée.

### Brouillard
Le brouillard ({{<unity_keyword `Fog` >}}) dans une scène 3D offre plusieurs avantages :
- il permet de cacher les éléments éloignés de la caméra, et donc d'éviter les effets de {{<unity_keyword `clipping` >}} (lorsqu'un objet dépasse soudainement le {{<unity_keyword `far clipping plane` >}});
- il permet de mettre en évidence les objets qui sont aux premier-plan, par rapport aux éléments plus éloignés de la caméra.

## Ombres
Les ombres sont un élément essentiel de toute scène 3D.
Ce sont elles qui donnent l'information de profondeur.
En particulier, sans les ombres nous avons souvent l'impression que les objets flottent au lieu d'être posés sur une surface.
La technique principale pour calculer les ombres est appelée {{<unity_keyword `Shadow Mapping` >}}
Elle consiste à faire un pseudo-rendu de la scène en positionnant la caméra sur chacune des lumières.
Ainsi, on peut calculer toutes les surfaces vues (et donc éclairées) pour chaque lumière.
Le résultat de ce calcul correspond en fait à la {{<unity_keyword `Depth Map` >}} calculée durant le rendu.
Dans le cas du calcul d'ombres, on parle plutôt de {{<unity_keyword `Shadow Map` >}}.
Dans un deuxième temps, grâce aux différentes {{<unity_keyword `Shadow Maps` >}} calculées, on peut rapidement déduire les parties ombragées, et ceci pour chaque lumière.

Les ombres sont configurables de 3 manières différentes :
1. les paramètres de qualité des ombres. Ils sont globaux et appliqués à toute la scène;
2. les paramètres liés à chaque objet;
3. et enfin les paramètres liés à chaque lumière.

Les paramètres de qualité des ombres sont stockés dans des {{<unity_keyword `Assets` >}}.
En allant dans le répertoire {{<unity_menu `Assets/Settings` >}}, on peut trouver plusieurs {{<unity_keyword `Assets` >}} contenant les paramètres de qualité pour le rendu.

{{<hint warning >}}
**ATTENTION**

Il est important de sélectionner le bon {{<unity_keyword `Asset` >}} en fonction de celui qui est appliqué dans le projet.
Pour ce faire, il faut regarder dans les {{<unity_keyword `Project Settings` >}} puis dans la section {{<unity_keyword `Quality` >}}.
{{</hint >}}

En sélectionnant {{<unity_keyword `Universal Render Pipeline` >}} (le nom peut varier), la section concernant les ombres ressemble à la figure qui suit :
{{<figure src="images/UnityURPShadowSettings.png#center" >}}

En sélectionnant le {{<unity_keyword `GameObject` >}} qui nous intéresse, alors on peut consulter le {{<unity_keyword `Mesh renderer` >}} associé.
En particulier, il contient les paramètres pour définir les ombres spécifiquement à ce {{<unity_keyword `GameObject` >}} comme indiqué sur la figure qui suit :
{{<figure src="images/UnityMeshRendererComponent.png#center" >}}

Enfin, on peut configurer les ombres projetées pour chaque lumière.
Pour ce faire, il faut aller dans le {{<unity_keyword `Light Component` >}} et modifier les paramètres présents :
{{<figure src="images/UnityLightComponentShadows.png#center" >}}

## Slides
{{<slides "http://enseignement.pages.ing.he-arc.ch/isc/cours/niveau-3/3292.2-infographie-unity/slides/Chap2_CamerasMateriauxEtIllumination.html">}}

## Références
[^1]: [Lights, Unity](https://docs.unity3d.com/Manual/class-Light.html)
[^2]: [The Lighting window, Unity](https://docs.unity3d.com/Manual/lighting-window.html)



