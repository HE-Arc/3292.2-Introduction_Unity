---
title: "Chapitre 2.1 : caméras"
---
# Chapitre 2.1 : caméras
Les caméras spécifient comment les objets 3D sont projetés (transformés) sur l'écran 2D.
Elles définissent donc quels objets 3D seront visibles par l'utilisateur final.

{{<hint warning >}}
**Built-in, Universal and High Definition Render Pipelines**

Dans Unity, les {{<unity_keyword Components>}} de type {{<unity_keyword Camera>}} sont différents en fonction du {{<unity_keyword `Render Pipeline`>}} utilisé.
Dans ce cours, nous nous focalisons sur URP.
Des liens sur la documentation relative aux {{<unity_keyword Cameras>}} pour le {{<unity_keyword `Built-in Render Pipeline`>}} et pour le {{<unity_keyword `High Definition Render Pipeline`>}} se trouvent dans les références.
{{</hint >}}

Dans Unity, les {{<unity_keyword Cameras>}}[^UnityURPCamera] sont composées et représentées de la manière suivante :
{{<figure src="images/UnityCamera.png#center">}}
On peut en particulier noter :
1. le {{<unity_keyword Gizmo>}} de la {{<unity_keyword Camera>}} et son icône associée dans la scène 3D;
2. le frustum de la {{<unity_keyword Camera>}};
3. une fenêtre de preview visible dans la scène 3D lorsque qu'une {{<unity_keyword Camera>}} est sélectionnée;
4. le {{<unity_keyword Component>}} {{<unity_keyword Camera>}} qui contient les paramètres importants.

Il est important de rappeler qu'une {{<unity_keyword Camera>}} est un {{<unity_keyword GameObject>}} et contient donc au moins un {{<unity_keyword Transform>}}.
En particulier, une {{<unity_keyword Camera>}} peut être déplacée, tournée, et même être parentée à un autre {{<unity_keyword GameObject>}}.

{{<hint info >}}
**Aligner une caméra avec la vue interactive (et vice versa)**

Il est important de bien positionner une {{<unity_keyword Camera>}} dans la scène 3D pour que la vue finale soit correcte.
La première étape est donc de bien définir les valeurs de son {{<unity_keyword Transform>}}.
Pour ce faire, on peut par exemple utiliser son {{<unity_keyword Gizmo>}}.
Une autre solution consiste à positionner la vue interactive dans la position désirée, puis de sélectionner l'outil {{<unity_menu `GameObject > Align With View` >}} dans la barre d'outils.
On peut aussi utiliser le racourci clavier {{<unity_menu `Ctrl+Shift+F` >}}.

Inversement, on peut aussi aligner la vue interactive avec la {{<unity_keyword Camera>}}.
Pour ce faire, il suffit de sélectionner la {{<unity_keyword Camera>}} dans la scène 3D, puis de sélectionner l'outil {{<unity_menu `GameObject > Align View With` >}} dans la barre d'outils.

{{</hint >}}

De manière simplifiée, on peut imaginer qu'une caméra prend des entrées, effectue des calculs, et stocke les résultats dans des sorties :
- **les entrées :** la liste d’objets 3D à projeter ainsi que les paramètres de la {{<unity_keyword Camera>}};
- **les sorties :** l'image finale ({{<unity_keyword `Color Buffer`>}}) et les informations de profondeur ({{<unity_keyword `Depth Buffer`>}} ou {{<unity_keyword `Z-Buffer`>}}).

Les paramètres les plus utiles du {{<unity_keyword Component>}} {{<unity_keyword Camera>}} sont :
- {{<unity_keyword `Projection / Projection`>}} : définit le type de projection à effectuer.
Elle peut-être perspective ou orthogonale.
- {{<unity_keyword `Projection / Field of View`>}} : correspond à l'angle de vue (horizontal ou vertical) de la {{<unity_keyword Camera>}}.
- {{<unity_keyword `Projection / Clipping Planes`>}} : ce paramètre permet d'ignorer les objets qui sont trop près ou au contraire trop éloignés.
- {{<unity_keyword `Environment / Background Type`>}} : spécifie la couleur ou l'image du fond.
C'est ce qui doit être affiché dans les espaces vides, c'est-à-dire les espaces de l'image finale dans lesquels aucun objet 3D n'est présent.
- {{<unity_keyword `Output / Viewport Rect` >}} : permet d'afficher l'image finale sur une sous-partie de l'écran seulement.

Certains paramètres offrent des fonctionnalités très intéressantes et méritent d'être un peu plus détaillés.

## Culling Mask
Le paramètre {{<unity_keyword `Rendering / Culling Mask` >}} permet de spécifier quels groupes d'objets 3D doivent être considérés (et donc rendus) par la {{<unity_keyword Camera>}}.
{{<figure src="images/UnityCameraCullingMask.png#center">}}

Un {{<unity_keyword `Culling Mask` >}} permet par exemple de créer des mini-maps avec une {{<unity_keyword Camera>}} qui fait le rendu de la scène 3D en vue du dessus, en ne considérant que certains objets particuliers.
Par exemple, on peut souhaiter ignorer le personnage principal, mais uniquement utiliser une représentation simplifiée sur la mini-map.

## Output Texture
Le paramètre {{<unity_keyword `Output / Output Texture` >}} permet de sauvegarder le rendu final dans une texture de rendu ({{<unity_keyword `Render Texture` >}}), plutôt que de l'afficher sur l'écran.
Cette {{<unity_keyword `Render Texture` >}} peut ensuite être réutilisée en temps-réel dans la scène 3D.

Pour attacher une {{<unity_keyword `Render Texture` >}} à une caméra par l'intermédiaire du paramètre ***Output Texture***, il faut d'abord la créer sous forme d'***Asset***.
Pour ce faire, il faut aller dans le menu {{<unity_menu `Assets/Create/Render Texture` >}}, comme indiqué sur l'image suivante :
{{<figure src="images/UnityCreateRenderTexture.png#center">}}

Les {{<unity_keyword `Render Textures` >}} sont utiles par exemple pour :
- avoir plusieurs rendus de {{<unity_keyword Camera>}} dans la même vue (vue top, left, right de la même scène);
- simuler des caméras de surveillance. On positionne des {{<unity_keyword Cameras>}} là où il y a des caméras de surveillance dans la scène 3D. Ensuite, les images calculées par les {{<unity_keyword Cameras>}} sont stockées en temps-réel dans des {{<unity_keyword `Render Texture` >}}. Ces textures sont finalement plaquées sur des objets 3D représentant des écrans dans la scène 3D.

## Slides
{{<slides "http://enseignement.pages.ing.he-arc.ch/isc/cours/niveau-3/3292.2-infographie-unity/slides/Chap2_CamerasMateriauxEtIllumination.html">}}

## Références
[^UnityBuiltInCamera]: [Cameras, Built-in Pipeline, Unity](https://docs.unity3d.com/Packages/com.unity.render-pipelines.universal@10.7/manual/cameras.html)
[^UnityURPCamera]: [Cameras, URP, Unity](https://docs.unity3d.com/Packages/com.unity.render-pipelines.universal@10.7/manual/cameras.html)
[^UnityHDRPCamera]: [Cameras, HDRP, Unity](https://docs.unity3d.com/Packages/com.unity.render-pipelines.high-definition@10.7/manual/index.html)