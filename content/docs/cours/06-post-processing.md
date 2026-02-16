---
title: "Chapitre 6 : post-processing"
---
# Chapitre 6 : post-processing
{{<teaservideo "http://enseignement.pages.ing.he-arc.ch/isc/cours/niveau-3/3292.2-infographie-unity/medias/Videos/Chapter6_final.mp4">}}

Les effets de {{<unity_keyword `Post-Processing` >}}[^UnityPostProcessing] sont appliqués à l'image rendue par la caméra dans la scène.
Ils sont très variés et permettent d'améliorer le rendu final de manière significative.
Il est par exemple possible de rajouter du flou de bougé ({{<unity_keyword `Motion Blur` >}}), d'échantillonner les couleurs, ou encore de rajouter un effet de vignettage.

Les effets de {{<unity_keyword `Post-Processing` >}} dépendent évidemment de l'image finale rendue.
Mais ils dépendent aussi de la position de la caméra dans la scène : il est ainsi possible d'activer certains effets en fonction de la position courante de cette dernière.

Pour activer le calcul des effets de {{<unity_keyword `Post-Processing` >}} pour la caméra qui nous intéresse, il faut sélectionner notre {{<unity_keyword `Camera` >}}, et dans la section {{<unity_keyword `Rendering` >}}, activer le paramètre {{<unity_keyword `Post Processing` >}} :
{{<figure src="images/UnityCameraPostProcessingSetting.png#center" >}}

Les effets de {{<unity_keyword `Post-Processing` >}} sont attachés à un {{<unity_keyword `Volume` >}} : quand la caméra entre dans ce {{<unity_keyword `Volume` >}}, les effets sont appliqués.
Pour commencer, nous pouvons créer un {{<unity_keyword `Global Volume` >}} : dans ce cas, les effets attachés à ce {{<unity_keyword `Volume` >}} sont toujours appliqués à la caméra.
Il faut donc aller dans le menu {{<unity_menu `GameObjects > Volume > Global Volume` >}} :
{{<figure src="images/UnityCreateVolumeMenu.png#center" >}}

Tous les paramètres de tous les effets de {{<unity_keyword `Post-Processing` >}} d'un {{<unity_keyword `Volume` >}} sont stockés dans un {{<unity_keyword `Profile` >}}.
Dans un premier temps, il faut donc créer un {{<unity_keyword `Profile` >}} et l'attacher au {{<unity_keyword `Volume` >}}.
Pour ce faire, il suffit d'aller sur le paramètre {{<unity_keyword `Profile` >}} de notre {{<unity_keyword `Volume` >}} et de cliquer sur le bouton {{<unity_button `New` >}} :
{{<figure src="images/UnityCreateNewProfileButton.png#center" >}}

Le {{<unity_keyword `Profile` >}} est automatiquement créé et attaché au {{<unity_keyword `Volume` >}}.
De plus, tous les paramètres sont automatiquement initialisés avec des valeurs par défaut, et sont tous initialement cachés.

Pour modifier les paramètres des effets de {{<unity_keyword `Post-Processing` >}}, il faut donc ajouter des {{<unity_keyword `Overrides` >}} au {{<unity_keyword `Profile` >}}.
Ceci se fait en cliquant sur le bouton {{<unity_button `Add Override` >}} dans le {{<unity_keyword `Volume` >}} :
{{<figure src="images/UnityAddOverrideButton.png#center" >}}

Il y a un {{<unity_keyword `Override` >}} par effet de {{<unity_keyword `Post-Processing` >}}.
Il existe beaucoup d'effets disponibles et ils dépendent du pipeline de rendu utilisé.
La vidéo suivante détaille la plupart des effets et leur impact sur le rendu final de la caméra pour le pipeline de rendu URP :
<center>
<iframe width="734" height="413" src="https://www.youtube.com/embed/9tjYz6Ab0oc?start=220"
frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</center>

Il est possible de modifier le mode de fonctionnement du {{<unity_keyword `Volume` >}} utilisé.
Il faut pour cela éditer le paramètre {{<unity_keyword `Mode` >}} du {{<unity_keyword `Volume` >}} :
{{<figure src="images/UnityVolumeModeSetting.png#center" >}}

Une fois le {{<unity_keyword `Volume` >}} en mode {{<unity_keyword `Local` >}}, il faut lui attacher un {{<unity_keyword `Collider` >}} :
{{<figure src="images/UnityVolumeAddCollider.png#center" >}}
Maintenant, quand la caméra entrera dans l'espace défini par ce {{<unity_keyword `Collider` >}}, les effets de {{<unity_keyword `Post-Processing` >}} seront appliqués.

## Slides
{{<slides "http://enseignement.pages.ing.he-arc.ch/isc/cours/niveau-3/3292.2-infographie-unity/slides/Chap6_Post-processing.html">}}

## Références

[^UnityPostProcessing]: [Post-processing in the Universal Render Pipeline, Unity](https://docs.unity3d.com/Packages/com.unity.render-pipelines.universal@10.2/manual/integration-with-post-processing.html)
