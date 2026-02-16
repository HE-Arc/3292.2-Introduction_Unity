---
title: "Chapitre 2.2 : matériaux"
---

# Chapitre 2.2 : matériaux
Les {{<unity_keyword Materials >}}[^1] définissent l'aspect visuel des {{<unity_keyword GameObjects >}} dans Unity.
Ils contiennent donc les informations nécessaires pour calculer les rendus.

Un {{<unity_keyword Material >}} contient les éléments suivants :
{{<figure src="images/UnityMaterial.png#center" >}}

1. un {{<unity_keyword Shader >}} qui est chargé de faire les calculs pour le rendu à proprement parler. Nous verrons les {{<unity_keyword Shaders >}} dans un chapitre dédié au [{{<unity_keyword `Shader Graph` >}}](../07-shadergraph);
2. des {{<unity_keyword Textures >}}[^2] qui représentent les données dont le {{<unity_keyword Shader >}} a besoin pour le rendu;
3. des paramètres qui sont injectés au {{<unity_keyword Shader >}} pour contrôler le rendu.

Il existe déjà beaucoup de {{<unity_keyword Shaders >}} et de {{<unity_keyword Materials >}} livrés avec Unity ou disponible directement sur l'{{<unity_keyword `Asset Store` >}}[^3] de Unity.

{{<hint warning >}}
**In-Editor Asset Store Unity 2020.1**  
Contrairement à ce qui est indiqué dans la documentation, l'{{<unity_keyword `Asset Store` >}} n'est plus disponible dans l'éditeur Unity depuis la version 2020.1.
Il faut passer par le site web directement.
{{</hint >}}

Dans Unity, il existe plusieurs [{{<unity_keyword `Render Pipelines` >}}]({{< ref "Les-Pipelines-de-rendu-dans-Unity.md" >}}).
Dans le cadre de ce cours, nous utiliserons le {{<unity_keyword `Universal Render Pipeline` >}} (URP).
Il faut donc faire attention de créer et d'utiliser des {{<unity_keyword Shaders >}} et des {{<unity_keyword Materials >}} compatibles.

Il existe plusieurs {{<unity_keyword Shaders >}} disponibles avec URP[^5].
En particulier, le {{<unity_keyword `Lit Shader` >}}[^6] offre beaucoup de possibilités et permet très souvent d'obtenir les résultats souhaités.
Dans les cas où le rendu final n'a pas besoin d'être proche de la réalité, ou sur des architectures limitées en puissance, alors le  {{<unity_keyword `Simple Lit Shader` >}}[^7] est approprié.

Les figures suivantes montrent un exemple de {{<unity_keyword Material >}} utilisant le {{<unity_keyword `Lit Shader` >}} (à gauche), et le {{<unity_keyword `Simple Lit Shader` >}} (à droite ) :

{{< columns >}}
{{<figure src="images/UnityURPLitShader.png#center" >}}
<--->
{{<figure src="images/UnityURPSimpleLitShader.png#center" >}}
{{< /columns >}}

Les {{<unity_keyword Materials >}} sont des {{<unity_keyword `Assets` >}} qui pourront être appliqués à plusieurs {{<unity_keyword `GameObjects` >}} différents à la fois.
Pour les créer, il faut donc aller dans le menu {{<unity_menu `Assets/Create/Material` >}} et choisir le {{<unity_keyword Shader >}} désiré.
Il ne reste plus qu'à l'appliquer aux {{<unity_keyword `GameObjects` >}} désirés.
Pour ce faire, on peut :
- éditer le {{<unity_keyword `Mesh Renderer Component` >}};
- tout simplement faire un drag-and-drop sur l'objet 3D dans la scène.

## Slides
{{<slides "http://enseignement.pages.ing.he-arc.ch/isc/cours/niveau-3/3292.2-infographie-unity/slides/Chap2_CamerasMateriauxEtIllumination.html">}}

## Références
[^1]: [Creating and Using Materials, Unity](https://docs.unity3d.com/Manual/Materials.html)
[^2]: [Textures, Unity](https://docs.unity3d.com/Manual/Textures.html)
[^3]: [Using the Asset Store, Unity](https://docs.unity3d.com/Manual/AssetStore.html)
[^5]: [Shaders and Materials, Unity](https://docs.unity3d.com/Packages/com.unity.render-pipelines.universal@7.1/manual/shaders-in-universalrp.html)
[^6]: [Lit Shader, Unity](https://docs.unity3d.com/Packages/com.unity.render-pipelines.universal@7.1/manual/lit-shader.html)
[^7]: [Simple Lit Shader, Unity](https://docs.unity3d.com/Packages/com.unity.render-pipelines.universal@7.1/manual/simple-lit-shader.html)
