---
title: "Photoréalisme : les points importants"
author: "Benoit Le Callennec"
date: 2021-01-19
tags : [
    "General", "TLPL"
    ]
---
**Cet article résume les points les plus intéressants mentionnés dans les vidéos ci-dessous :**

<center>
<iframe width="734" height="413" src="https://www.youtube.com/embed/videoseries?list=PLoMYgUbrKKtdjwAfde9651W5zZZVTmPE6"
frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</center>

75% des images des catalogues IKEA sont en fait des images de synthèse photoréalistes (au lieu de photographies).
Les images de synthèse offrent une plus grande flexibilité.
Elles permettent surtout de visualiser des effets et des objets qui n'existent tout simplement pas dans la réalité.

Pour obtenir des images photoréalistes, il faut 4 éléments fondamentaux : modélisation, matériaux, illumination et post-processing.
Ces 4 éléments doivent être d'une excellente qualité pour obtenir des résultats convaincants.
De ces 4 domaines, les parties qui demandent le plus de temps et d'attention sont la création des matériaux, et l'illumination.
> ...90% of the time, the materials and lighting carry the weight of creating truly photorealism imagery. - **Alex Roman, From Bits to Lens**

## Modélisation
- Utiliser les vraies dimensions des objets;
- Éviter les arêtes trop fines, comme les cubes créés par défaut dans Unity par exemple;
- Utiliser des objets réels (références) pour modéliser les objets 3D;
- Pour modéliser des humains, il faut avoir d'excellentes connaissances en anatomie.

## Matériaux
- Utiliser des ***Materials / Shaders*** physiquement justes;
- Utiliser des ***Normal Maps / Bump Maps*** pour simuler les détails d'une surface;
- Simuler les imperfections des matériaux (verres, empreintes, poussière) avec des textures.

## Illumination
- Utiliser des lumières correspondant à des lumières réelles : par exemple, pour simuler le soleil, il est préférable d'essayer de lui donner la couleur et la direction réelle;
- Bien gérer les réflexions des matériaux.

## Post-Processing
- Simuler les ***light glares / lens flares***;
- Simuler le ***Motion Blur***;
- Bien gérer la profondeur de champs;
- Ajouter des aberrations chromatiques;
- Simuler les distorsions des lentilles des appareils photo.

## Gestion des couleurs / Dynamic range
La figure suivante (from Blender Guru) montre une estimation de la sensibilité des "capteurs photographiques" courants :
{{<figure src="images/fstopsComparisons.png#center" width="100%">}}

Il faut faire attention à ne pas utiliser sRGB (ancienne technique avec une dynamique limitée) et utiliser ACES qui est un standard de l'industrie.