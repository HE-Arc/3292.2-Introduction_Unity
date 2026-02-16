---
title: Les pipelines de rendu dans Unity
author: "Benoit Le Callennec"
date: 2020-09-13
tags : [
    "Unity", "Rendering"
]
---
{{<figure src="images/UnityRenderPipeline.png#center" width=100% >}}
Le **pipeline de rendu** (graphics pipeline ou rendering pipeline en Anglais)[^1] représente la suite d'étapes à effectuer pour transformer une scène 3D en points 2D sur l'écran (pixels).

Les étapes principales du pipeline de rendu pour OpenGL sont :
{{<figure src="images/RenderingPipeline.svg#center" width="60%" >}}

Unity propose 2 types de pipelines de rendu : 
- **Built-in Render Pipeline**[^2] : c'est le pipeline de rendu par défaut.
- **Scriptable Render Pipeline** (ou ***SRP***)[^3]  : c'est un pipeline de rendu configurable et pilotable grâce à des scripts C#.

La vidéo suivante résume les principales différences des pipelines de rendu dans Unity :
{{< youtube 2wUPgl7upnU >}}

On peut en particulier noter les avantages suivants concernant ***SRP*** :
- une plus grande flexibilité en ce qui concerne le rendu;
- un meilleur contrôle sur le rendu des objets et sur les performances en général.

Mais ***SRP*** requiert beaucoup de développements (et donc de temps) avant d'avoir quelque chose de fonctionnel.
De plus, chaque ***SRP*** est unique à chaque projet, et chaque plateforme.

Pour ces raisons, Unity offre 2 templates de ***SRP*** pré-construits et utilisables directement :
- **Universal Render Pipeline** (ou ***URP***, anciennement ***LWRP***)[^4] : ***SRP*** pré-configuré pour fonctionner sur un maximum de plateformes (mobiles, consoles, etc.);
- **High Definition Render Pipeline** (ou HDRP)[^5] : ***SRP*** pré-configuré pour fournir les meilleurs résultats visuels sur les plateformes les plus performantes (PS 4/5, Xbox One/X/S, Computer with Metal or Vulkan support, etc.). 

Les sections suivantes résument les avantages et les désavantages des 3 pipelines de rendu fournis par Unity.

## Built-in Render Pipeline
{{<figure src="images/UnityBuiltInRenderPipeline.png#center" width=100% >}}
Ce pipeline de rendu devrait suffire pour la grande majorité des développeurs.
Il existe beaucoup d'assets pré-existants (shaders, objets, scripts, etc.).
Néanmoins, le ***Built-in Render Pipeline*** n'offre pas une grande liberté pour modifier le rendu.
Enfin, **Shader Graph**[^6] et **VFX Graph**[^7] ne sont pas supportés.

## URP : Universal Render Pipeline
{{<figure src="images/URP.png#center" width=100% >}}
***URP*** offre de meilleures performances que le ***Built-in Render Pipeline***.
Il est compatible avec  un grand nombre d'architectures.
***URP*** est recommandé pour les applications 2D, XR et les plateformes mobiles.
De plus, ***URP*** remplacera à termes le ***Built-in Render Pipeline***.
Cependant, l'apprentissage est plus compliqué.
Enfin, les outils pré-existants ne sont pas tous encore compatibles.
## HDRP : High Definition Render Pipeline
{{<figure src="images/HDRP.png#center" width=100% >}}
***HDRP*** optimise les rendus pour les architectures haute performance comme les PCs et les consoles de jeux.
Il offre plus de possibilités pour les shaders, l'illumination, le post-processing, etc.
Enfin, ***HDRP*** supporte le "**real-time Ray Tracing**"[^8] et la technologie RTX.
Cependant, tout comme ***URP***, l'apprentissage est plus compliqué.
De même, les outils pré-existants ne sont pas tous encore compatibles.

## Références
[^1]: [Graphics Pipeline, Wikipedia](https://en.wikipedia.org/wiki/Graphics_pipeline)
[^2]: [Built-in Render Pipeline, Unity](https://docs.unity3d.com/Manual/built-in-render-pipeline.html)
[^3]: [Scriptable Render Pipeline, Unity](https://docs.unity3d.com/Manual/ScriptableRenderPipeline.html)
[^4]: [Universal Render Pipeline, Unity](https://docs.unity3d.com/Manual/universal-render-pipeline.html)
[^5]: [High Definition Render Pipeline, Unity](https://docs.unity3d.com/Manual/high-definition-render-pipeline.html)
[^6]: [Shader Graph, Unity](https://unity.com/shader-graph)
[^7]: [VFX Graph, Unity](https://unity.com/visual-effect-graph)
[^8]: [Unity real-time Ray Tracing, Unity](https://unity.com/ray-tracing)
