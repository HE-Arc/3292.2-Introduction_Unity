---
title: Commencer avec URP
author: "Benoit Le Callennec"
date: 2020-11-12
tags : [
    "Unity", "Rendering"
    ]
---
{{<hint danger >}}
**Dépréciée depuis Unity 2021**  
Depuis Unity 2021, il existe un template vide pour ***URP***.
Il n'est dont plus nécessaire d'effectuer les étapes détaillées dans cette page.
{{</hint >}}

Le pipeline de rendu utilisé dans ce cours est le ***Universal Render Pipeline*** (ou ***URP***)[^1].
Il faut donc créer un projet Unity avec une configuration particulière pour pouvoir l'utiliser.
Bien que la documentation Unity suggère d'utiliser le template fourni[^2] pour créer un projet basé sur ***URP***, celui-ci contient beaucoup de choses dont nous n'aurons pas besoin.
Ainsi, nous conseillons plutôt de commencer avec un projet vide (utilisant le ***Built-in Render Pipeline***), puis de le configurer pour qu'il utilise ***URP***[^3].

{{<hint warning >}}
**Transférer un projet existant vers URP**  
Il existe certaines limitations à utiliser ***URP***.
En particulier, ce pipeline de rendu utilise son propre système pour le post-processing. 
Dans ce cas, avant de transférer un projet vers ***URP***, il faut dans un premier temps effacer le package de post-processing existant.
{{</hint >}}

Pour créer un projet utilisant ***URP***, il faut donc suivre les étapes suivantes :
1. créer un projet vide en utilisant le template intitulé "3D" :
{{<figure src="images/UnityBuiltInRenderPipeline.png#center" width="100%">}}
ceci créera donc un projet basé sur le ***Built-in Render Pipeline***;
2. **[optionnel]** : rajouter un objet 3D dans la scène pour pouvoir rapidement vérifier que le changement de pipeline est effectif;
2. installer le package "Universal RP" :
{{<figure src="images/UnityURPPackage.png#center" width="100%">}}
3. créer un ***Asset*** de type ***Pipeline*** comme indiqué sur la figure suivante :
{{<figure src="images/UnityCreateURPAsset.png#center" width="100%">}}
4. configurer Unity pour qu'il utilise ce nouveau pipeline. Pour ce faire, il faut aller dans ***Edit/Project Settings.../Graphics*** et dans le paramètre ***Scriptable Render Pipeline Settings***, choisir le pipeline nouvellement créé.

Unity devrait maintenant utiliser le nouveau pipeline de rendu.
La conséquence directe est que les matériaux basés sur le ***Built-in Render Pipeline*** ne sont plus supportés.
Ainsi, si vous avez des objets dans votre scène initiale, ils devraient avoir maintenant une couleur magenta.
Si vous créez de nouveaux objets 3D, ils vont maintenant utiliser les nouveaux shaders compatibles avec ***URP***.
Ainsi, ils auront la couleur attendue comme visible sur la figure suivante (à gauche un cube créé avec l'ancien pipeline, à droite un cube créé avec ***URP***) :
{{<figure src="images/UnityCubeMaterialError.png#center" width="100%">}}

## Références
[^1]: [About the Universal Render Pipeline, Unity](https://docs.unity3d.com/Packages/com.unity.render-pipelines.universal@7.1/manual/index.html)
[^2]: [Using the Universal Render Pipeline in a new Project, Unity](https://docs.unity3d.com/Packages/com.unity.render-pipelines.universal@7.1/manual/creating-a-new-project-with-urp.html)
[^3]: [Installing the Universal Render Pipeline into an existing Project, Unity](https://docs.unity3d.com/Packages/com.unity.render-pipelines.universal@7.1/manual/InstallURPIntoAProject.html)


