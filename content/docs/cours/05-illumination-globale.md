---
title: "Chapitre 5 : illumination globale"
---

# Chapitre 5 : illumination globale

Dans ce chapitre, nous allons nous intéresser aux techniques permettant d'améliorer le rendu final de notre scène 3D.
Il est tout d'abord important de bien faire la différence entre 2 types d'illuminations :

- l'**illumination directe**, qui s'intéresse aux interactions directes entre les lumières et les objets;
- l'**illumination indirecte**, qui s'intéresse aux interactions indirectes entre les lumières et les objets. 

Par exemple, quand une lumière illumine un objet qui à son tour influence l'illumination d'un autre objet alors on parle d'**illumination indirecte**.

L'illumination globale est un ensemble de techniques permettant de considérer la **lumière indirecte** c'est-à-dire celle qui est donc réfléchie par les différentes surfaces de la scène 3D (autres que les lumières).
Ces algorithmes sont pour la plupart difficiles à implémenter et surtout coûteux en temps de calcul.

L'idée générale est de tirer partie des informations de la scène 3D pour effectuer (et stocker) le plus de calculs possibles (pré-calculs) relatifs à la lumière, avant de lancer l'application.
Ces informations précalculées sont appelées des {{<unity_keyword `Lightmaps` >}}.
De plus, quand on précalcule on dit souvent qu'on {{<unity_keyword `Bake` >}}.
Ces {{<unity_keyword `Lightmaps` >}} sont ensuite réutilisées en temps-réel pour améliorer l'illumination de la scène 3D.

La figure suivante montre la différence entre une scène 3D qui ne considère que l'illumination directe (avec des réflexions) à gauche et une scène qui prend aussi en compte l'illumination globale :
{{< columns >}}
**Illumination directe** (avec réflexions)
{{<figure src="images/GI_OFF.png#center" >}}
<--->
**Illumination globale** ajoutée
{{<figure src="images/GI_ON.png#center" >}}
{{< /columns >}}
On peut en particulier noter le sol vert qui "illumine" les murs blancs.
On voit aussi que les intersections des murs sont plus ombragées.

Il est cependant important de prendre en compte une contrainte forte : le tout doit être calculable **en temps-réel**, c'est à dire au minimum 30 fois par secondes.
Ainsi, pour qu'une application 3D soit considérée comme temps-réelle, il faut que chaque image soit calculable en moins de 16.67ms.
Pour comparaison, le film Coco de Pixar a demandé pour les scènes les plus complexes [55 heures de calcul par image]({{< relref "/posts/Coco-de-Pixar-quelques-chiffres" >}}).
Il est donc important de comprendre que le niveau de réalisme visé n'est pas comparable à celui atteint pour les films (qui sont eux entièrement précalculés).

## Lighting Settings PREVIEW et FINAL

Le calcul de ces {{<unity_keyword `Lightmaps` >}} se fait dans l'éditeur de Unity directement.
Cependant, si les {{<unity_keyword `Lightmaps` >}} sont très détaillées, alors elles vont demander beaucoup de temps de **précalcul** mais donneront un résultat réaliste à l'exécution.
C'est ce que nous souhaitons dans la version finale de notre application.
Au contraire, si elles sont peu détaillées, elles seront rapides à **précalculer** mais donneront des résultats plus grossiers à l'exécution.
C'est ce que nous souhaitons lorsque l'on travaille encore sur l'application et que l'on souhaite rapidement pré-visualiser les résultats.

Nous allons donc créer 2 {{<unity_keyword `Lighting Settings` >}}.
Pour ce faire, il faut aller dans menu {{<unity_menu `Window > Rendering > Lighting` >}} :
{{<figure src="images/UnityLightingWindowMenu.png#center" >}}

Ensuite, en cliquant sur le bouton {{<unity_button `New Lighting Settings` >}}, nous pouvons définir des valeurs de paramètres pour l'illumination.

Voici 2 exemples de configurations pour la prévisualisation et le rendu final :
{{< columns >}}
**Configuration pour la prévisualisation**
{{<figure src="images/UnityLightingSettingsPREVIEW.png#center" >}}
<--->
**Configuration pour le rendu final**
{{<figure src="images/UnityLightingSettingsFINAL.png#center" >}}
{{< /columns >}}
Notez que l'on passe de 13 secondes pour précalculer les {{<unity_keyword `Lightmaps` >}} en mode prévisualisation à plus de 5 minutes en mode rendu final.

## Objets 3D statiques

Si les objets de la scène sont mobiles (donc dynamiques), la lumière changera aussi de manière dynamique et rien (ou très peu) ne pourra être précalculé.
Au contraire, si les objets 3D sont immobiles (statiques) dans la scène, alors on peut utiliser cette information pour précalculer leur illumination.

Il faut donc marquer les objets immobiles comme {{<unity_keyword `static` >}} dans Unity pour qu'ils soient pris en compte dans le calcul de l'illumination globale :
{{<figure src="images/UnityInspectorStatic.png#center" >}}

## Lumières statiques et lumières dynamiques

De la même manière que pour les objets 3D, les lumières peuvent être statiques, ou dynamiques.
Dans Unity, les {{<unity_keyword `Lights` >}} peuvent en effet avoir 3 modes [^UnityLightModes]:

- {{<unity_keyword `Realtime` >}} (dynamique) : cette {{<unity_keyword `Light` >}} est calculée en temps-réel uniquement et ne contribue pas à l'illumination globale;
- {{<unity_keyword `Baked` >}} (statique) : cette {{<unity_keyword `Light` >}} n'est **pas** calculée en temps-réel.
Cependant, elle est prise en compte dans le calcul de l'illumination globale;
- {{<unity_keyword `Mixed` >}} (mixée) : cette {{<unity_keyword `Light` >}} est calculée en temps-réel **et** est prise en compte dans le calcul de l'illumination globale.

Pour chaque {{<unity_keyword `Light` >}}, il faut ajuster son mode en fonction des effets désirés :
{{<figure src="images/UnityLightBaked.png#center" >}}

## Occlusion Ambiante

L'occlusion ambiante (ou {{<unity_keyword `Ambient Occlusion` >}}) dans Unity permet de simuler l'impact sur l'illumination qu'ont des surfaces voisines.
Par exemple, 2 surfaces à angle droit auront tendance un atténuer la lumière arrivant à la jonction.
L'{{<unity_keyword `Ambient Occlusion` >}} peut être précalculée en modifiant les paramètres suivants :
{{<figure src="images/UnityLightingSettingsAO.png#center" >}}

Il faut noter qu'il est possible d'estimer l'{{<unity_keyword `Ambient Occlusion` >}} lors de la phase de post-processing, donc en temps-réel.
Ce sujet n'est pas couvert dans ce chapitre.

## Light Probes

L'illumination globale ne concerne que les objets statiques ainsi que les {{<unity_keyword `Lights` >}} dont le mode est {{<unity_keyword `Baked` >}} ou {{<unity_keyword `Mixed` >}}.
Dans ces conditions, un objet dynamique ne peut pas être influencé par l'illumination globale.
Il existe cependant une alternative : précalculer les informations relatives à l'illumination globale à certains points dans la scène 3D.
Puis réutiliser ces informations en temps-réel pour illuminer les objets dynamiques.
Pour ce faire, il faut créer des {{<unity_keyword `Light Probes Group` >}} :
{{<figure src="images/UnityLightProbeGroupMenu.png#center" >}}

Le {{<unity_keyword `Light Probes Group` >}} ainsi créé ressemble à ce qui suit dans l'{{<unity_keyword `Inspector` >}} :
{{<figure src="images/UnityLightProbeGroupComponent.png#center" >}}

Il est enfin nécessaire de modifier chaque {{<unity_keyword `Light Probe` >}} individuellement pour les placer aux endroits nécessaires.
Pour activer le mode d'édition, il faut d'abord cliquer sur le bouton {{<unity_button `Edit Light Probes` >}}.

## Slides

{{<slides "http://enseignement.pages.ing.he-arc.ch/isc/cours/niveau-3/3292.2-infographie-unity/slides/Chap5_IlluminationGlobale">}}

## Références

[^UnityLightModes]: [Light Mode, Unity](https://docs.unity3d.com/Manual/LightModes.html)
