---
title: ShaderLab
author: "Benoit Le Callennec"
date: 2020-09-06
tags : [
    "Unity",
    "Shaders",
]
draft: true
---
ShaderLab[^1] est un langage déclaratif utilisé pour écrire les shaders dans Unity.
Le code du shader en tant que tel, écrit en HLSL[^2], se situe entre les balises ***CGPROGRAM*** et ***ENDCG***.

{{< highlight cpp "linenos=table,hl_lines=4 11" >}}
Pass {
      // ... the usual pass state setup ...
      
      CGPROGRAM
      // compilation directives for this snippet, e.g.:
      #pragma vertex vert
      #pragma fragment frag
      
      // the Cg/HLSL code itself
      
      ENDCG
      // ... the rest of pass setup ...
  }
{{< / highlight >}}

## Références
[^1]: [ShaderLab Syntax](https://docs.unity3d.com/Manual/SL-Shader.html)
[^2]: [High-Level Shading Language](https://en.wikipedia.org/wiki/High-Level_Shading_Language)

