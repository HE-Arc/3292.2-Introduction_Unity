---
title: "Chapitre 8 : Interfaces Graphiques"
draft: true
---

# Chapitre 8 : Interfaces Graphiques

Il existe plusieurs façons de créer des interfaces graphiques dans Unity :
- {{<unity_keyword `Unity UI package (uGUI)` >}} : c'est l'outil historique de Unity pour créer des interfaces graphiques.
Il utilise des {{<unity_keyword `Canvas` >}} ainsi que des {{<unity_keyword `GameObject` >}} qui sont ajoutés et édités directement dans la scène.
- {{<unity_keyword `IMGUI (Immediate Mode GUI)` >}} : ce système permet de créer des GUI programmatiquement, c'est-à-dire directement depuis des scripts C#, dans une fonction appelée  se base sur des scripts C# exécutés à chaque frame pour créer des interfaces graphiques.
En particulier, il faut écrire le code qui va créer les éléments graphiques ainsi que les interactions directement dans une fonction `OnGUI()`.
-  {{<unity_keyword `UI Toolkit` >}}[^UnityUIToolkit]: c'est le nouveau système d'Unity pour créer des interfaces graphiques.
Il reprend les concepts de bases des interfaces web avec une séparation entre la structure et le style.

{{<hint warning >}}
**ATTENTION**  
Le {{<unity_keyword `UI Toolkit` >}} était initialement appelé {{<unity_keyword `UI Elements` >}}.
{{</hint >}}

Dans ce chapitre, nous allons voir comment utiliser {{<unity_keyword `UI Toolkit` >}} car les autres systèmes sont destinés à être dépréciés.

Il faut enfin noter qu'il existe 2 types d'interfaces graphiques :
- Les Editor UI : ce sont les interfaces graphiques qui sont utilisées dans l'éditeur Unity.
Elles permettent par exemple d'automatiser certaines tâches ou de créer des outils personnalisés directement dans l'éditeur Unity.
- Les Runtime UI : ce sont les interfaces graphiques qui sont utilisées directement dans l'application 3D finale.

## Editor UI



## Slides

{{<slides "http://enseignement.pages.ing.he-arc.ch/isc/cours/niveau-3/3292.2-infographie-unity/slides/Chap7_ShaderGraph.html">}}

## Références

[^UnityUIToolkit]: [UI Toolkit, Unity](https://docs.unity3d.com/Manual/UIElements.html)
