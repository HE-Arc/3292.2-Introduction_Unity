---
title: "Chapitre 1.1 : prise en main"
---

# Chapitre 1.1 : prise en main
Dans ce chapitre, nous considérons qu'un projet utilisant le pipeline de rendu ***Universal Render Pipeline***[^1] est déjà créé :
{{<figure src="images/UnityHubCreateProject.png#center" width="100%">}}

Pour des raisons pratiques, nous utilisons directement le template fourni par Unity.
Cependant, il est en général conseillé de commencer avec ***URP*** en utilisant un projet vide.

## Interface Générale
Lorsque vous démarrez votre projet pour la première fois, vous avez une fenêtre qui ressemble à ce qui suit :
{{<figure src="images/UnityInterfaceGeneral.png#center" width="100%">}}

Dans les sections qui suivent, nous passons en revue les principales fenêtres de Unity.

## Project Window
La fenêtre ***Project***[^2] ressemble à ceci :
{{<figure src="images/UnityInterfaceProjectWindow.png#center" width="100%">}}
Elle rassemble tout le contenu à votre disposition pour ce projet : on parle d'***Assets***.
Un ***Asset*** peut être toute donnée (en général un fichier) utilisable dans votre projet (images, modèles 3D, animations, etc.).
Il existe déjà beaucoup d'***Assets*** disponibles dans Unity ou sur l'***Asset Store***.
Ces ***Assets*** sont organisés grâce à une hiérarchie de répertoires pour un accès facilité.

## Scene View
La ***Scene View*** est une vue **interactive** [^3] et ressemble à ceci :
{{<figure src="images/UnityInterfaceSceneWindow.png#center" width="100%">}}

Les principales commandes pour la navigation sont :
- `alt` + bouton gauche | milieu | droit de la souris ainsi que la roulette pour naviguer en 3D;
- `F` pour centrer la caméra sur l'objet sélectionné;
-  `Shift + F` pour verrouiller la vue sur l'objet sélectionné.

Il existe beaucoup d'autres options consultables directement dans la documentation [^4].

Quand on parle de 3D, un ***gizmo*** permet de modifier l'orientation, la position et parfois les échelles de l'objet auquel il est attaché.
En particulier, le ***scene gizmo*** permet de manipuler la caméra courante :
{{<figure src="images/UnitySceneGizmo.png">}}
En faisant un clic droit sur le ***scene gizmo***, on peut afficher les vues prédéfinies disponibles pour la caméra courante :
{{<figure src="images/UnityPredefinedViews.png">}}
Il est enfin possible de bloquer l'orientation et la perspective de la caméra courante en cliquant sur le cadenas en haut à droite du ***scene gizmo***.

Voici un exemple de navigation en 3D en utilisant les commandes précédemment présentées :
{{<youtube YdJoH3u1Od4 >}}

## Game View
La ***Game View*** est la vue finale 3D de votre application [^5] :
{{<figure src="images/UnityInterfaceGameWindow.png#center" width="100%">}}
Il est possible de contrôler l'état du jeu (***Play*** | ***Pause*** | ***Step***) en utilisant les boutons suivants :
{{<figure src="images/UnityPlaybackControls.png#center" width="40%">}}

{{<hint danger >}}
**ATTENTION**  
tout changement à la scène en mode ***Play*** est temporaire et sera annulé lorsque l'on quitte l'application.
{{</hint >}}

## Hierarchy Window
La fenêtre ***Hierarchy*** contient tous les ***GameObjects*** contenus dans votre application [^6] :
{{<figure src="images/UnityInterfaceHierarchyWindow.png#center" width="100%">}}
Cette fenêtre organise les éléments sous forme de hiérarchie.
Elle est très utile pour sélectionner des ***GameObjects***, les (re)parenter et les cacher.

## Inspector Window
La fenêtre ***Inspector*** affiche les informations détaillées du ***GameObject*** sélectionné [^7] :
{{<figure src="images/UnityInterfaceInspectorWindow.png#center" width="100%">}}
Elle est très utile pour voir et modifier :
- les paramètres de ***GameObjects*** et de ***Components***;
- les paramètres des ***Assets***;
- la façon dont les ***Assets*** sont importés dans Unity;
- les variables publiques (ou sérialisées) des scripts.

## Toolbar
La ***Toolbar*** rassemble plusieurs boutons pour les outils les plus utilisés [^8] :
{{<figure src="images/UnityInterfaceToolbar.png#center" width="100%">}}

## Build & Run
Pour générer l'exécutable final de votre application 3D, il faut aller dans le menu `File / Build Settings` (aussi atteignable avec le raccourcis `Ctrl + Shift + B`) :
{{<figure src="images/UnityBuildSettings.png#center" width="100%">}}

On obtient une fenêtre qui ressemble à celle qui suit :
{{<figure src="images/UnityBuildSettingsWebGL.png#center" width="100%">}}

{{<hint info >}}
**À NOTER**  
Par défaut, le module permettant de générer des applications 3D en WebGL n'est pas installé.
Il faut donc d'abord l'installer depuis le ***Unity Hub***.
Une fois WebGL sélectionné, il suffit de cliquer sur `Switch Platform`.
{{</hint >}}

Il suffit ensuite de cliquer sur `Build and Run`.
Une fois l'application générée, vous devriez obtenir quelque chose comme ce qui suit :
{{< youtube zmn5nDf2dEc >}}

## Slides
{{<slides "http://enseignement.pages.ing.he-arc.ch/isc/cours/niveau-3/3292.2-infographie-unity/slides/Chap1_ConceptsFondamentaux.html">}}

## Références
[^1]: [Les pipelines de rendu dans Unity]({{< ref "/posts/Les-Pipelines-de-rendu-dans-Unity" >}})
[^2]: [The Project Window, Unity](https://docs.unity3d.com/Manual/ProjectView.html)
[^3]: [The Scene view, Unity](https://docs.unity3d.com/Manual/UsingTheSceneView.html)
[^4]: [Scene view navigation, Unity](https://docs.unity3d.com/Manual/SceneViewNavigation.html)
[^5]: [The Game view, Unity](https://docs.unity3d.com/Manual/GameView.html)
[^6]: [The Hierarchy window, Unity](https://docs.unity3d.com/Manual/Hierarchy.html)
[^7]: [The Inspector window, Unity](https://docs.unity3d.com/Manual/UsingTheInspector.html)
[^8]: [The Toolbar, Unity](https://docs.unity3d.com/Manual/Toolbar.html)
