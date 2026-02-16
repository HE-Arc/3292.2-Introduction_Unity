---
title: "Chapitre 4.1 : animation de personnages 3D"
---

# Chapitre 4.1 : animation de personnages 3D

L'animation 3D englobe beaucoup de domaines, chacun avec ses propres techniques et spécificités.
On peut noter par exemple :

- l'animation de fluides (liquides, gaz, etc.);
- l'animation de visages;
- l'animation de particules;
- l'animation de corps rigides (pierres qui roulent, collisions, etc.);
- et l'animation de personnages.

Il faut aussi noter que certaines de ces techniques sont calculables en temps-réel alors que d'autres sont trop complexes et doivent être pré-calculées.
Enfin, certaines techniques sont hybrides : elles pré-calculent une partie des résultats, et les réutilisent en temps-réel pour finaliser l'animation.

La vidéo suivante par exemple montre une animation de fluide (calculée en temps-réel) :
{{< youtube s-cDYtNfsl4 >}}

Ici, les lois de la physique sont utilisées pour calculer les mouvements de fourrure (toujours en temps-réel) :
{{< youtube OdT2CUGBBkI >}}

Enfin, la vidéo suivante montre une simulation physique de corps rigides (encore en temps-réel) :
{{< youtube xJVwDwIkaM4 >}}

Dans cette section, nous allons nous concentrer sur l'animation de personnages en 3D et en temps-réel, comme ce qui est montré sur la vidéo suivante :
{{< youtube gNDrjR45DGY >}}

Ce que nous allons faire dans cette section :

1. trouver des données d'animations 3D existantes;
2. créer un système pour animer notre personnage 3D. On parle de moteur d'animation;
3. contrôler notre moteur d'animation en fonction des événements déclenchés (entrées de l'utilisateur, collisions, etc).

## Trouver des données d'animations 3D

Créer des animations 3D est très compliqué et demande beaucoup de temps.
En particulier, chaque personnage 3D nécessite une configuration spécifique pour l'animation 3D.
Dans de nombreuses situations, il est donc trop complexe (et trop coûteux) de créer des animations 3D spécifiquement pour notre application.
Heureusement, il existe beaucoup d'animations 3D téléchargeables et directement utilisables dans Unity.

### Unity Asset Store

L'{{<unity_keyword `Asset Store` >}} de Unity possède de nombreuses animations 3D.
Dans cette section par exemple, nous allons utiliser le ***Zombie Animation Pack Free*** :
{{<figure src="images/UnityZombieAnimationPack.png#center" >}}

Nous allons en particulier utiliser le personnage 3D présent dans le répertoire `Assets/ZombieAnimationPackFree/Models/Appearance/BH-2/Mesh` :
{{<figure src="images/UnityAddZombie.png#center" >}}

### Mixamo

Mixamo[^Mixamo] est une base de données interactive contenant beaucoup d'animations 3D.
C'est une excellente solution car les données présentes sont gratuites.
Mixamo propose donc une excellente alternative à l'Asset Store de Unity.
{{<figure src="images/Mixamo.png#center" >}}

## Créer un moteur d'animation 3D

Dans Unity, un moteur d'animation 3D est représenté par un {{<unity_keyword `Animator Controller` >}}[^1].
Une fois créé, ce {{<unity_keyword `Component` >}} doit être connecté à l'{{<unity_keyword `Animator` >}} du personnage 3D que nous souhaitons animer comme le montre la figure qui suit :
{{<figure src="images/UnityAnimatorControllerComponent.png#center" >}}

Un {{<unity_keyword `Animator Controller` >}} est en fait une machine à états finis (un graphe) qui sert à :

1. gérer les clips d'animation 3D (on parle d'{{<unity_keyword `Animation Clips` >}}[^2]);
2. changer l'animation courante (celle en train d'être jouée) grâce aux {{<unity_keyword `State Machine Transitions` >}} et aux {{<unity_keyword `Triggers` >}}[^3];
3. mélanger les animations entre elles pour en créer de nouvelles en utilisant des {{<unity_keyword `Blend Trees` >}}.

Les {{<unity_keyword `Transitions` >}} permettent de changer d'animation active :

1. en temps-réel;
2. en fonction des entrées de l'utilisateur;
3. de manière fluide, sans secousse.

Pour créer un {{<unity_keyword `Animator Controller` >}}, il faut aller dans le menu {{<unity_menu `Assets > Create > Animator Controller` >}} comme indiqué sur la figure qui suit :
{{<figure src="images/UnityCreateAnimatorController.png#center" >}}

Il faut ensuite l'assigner à l'{{<unity_keyword `Animator` >}} du personnage 3D que l'on souhaite animer puis l'ouvrir dans l'éditeur (en double cliquant dessus par exemple).
Vous devriez obtenir une fenêtre ressemblant à la figure suivante :
{{<figure src="images/UnityEmptyAnimatorController.png#center" >}}

### État simple

Comme dit précédemment, un {{<unity_keyword `Animator Controller` >}} est une machine d'états finis.
Chaque état représente en fait une animation du personnage 3D.
Pour rajouter un nouvel état à l'{{<unity_keyword `Animator Controller` >}}, il suffit de faire un clic droit dans la fenêtre {{<unity_window `Animator` >}}, puis de sélectionner {{<unity_menu `Create State > Empty` >}} :
{{<figure src="images/UnityCreateNewState.png#center" >}}

À chaque état créé, on peut associer un {{<unity_keyword `Animation Clip` >}} comme indiqué sur la figure suivante :
{{<figure src="images/UnityAddMotionToState.png#center" >}}

Nous pouvons créer des transitions entre chaque état en faisant un clic droit sur l'état initial de la transition, en sélectionnant {{<unity_menu `Make Transition` >}}, puis en sélectionnant l'état d'arrivée :
{{<figure src="images/UnityMakeTransition.png#center" >}}

Enfin, nous pouvons rajouter des {{<unity_keyword `Triggers` >}} aux {{<unity_keyword `Transitions` >}} pour les activer lorsque certains événements sont déclenchés.
Pour créer un {{<unity_keyword `Trigger` >}}, il faut aller dans {{<unity_menu `Parameters` >}}, puis cliquer sur `+` et choisir {{<unity_menu `Trigger` >}} :
{{<figure src="images/UnityCreateTrigger.png#center" >}}

Pour le rajouter à une transition, il suffit de la sélectionner.
Puis dans l'{{<unity_window `Inspector` >}}, aller dans le bloc {{<unity_keyword `Conditions` >}} pour en rajouter une, et sélectionner le {{<unity_keyword `Triggers` >}} précédemment créé :
{{<figure src="images/UnityAddTriggerToTransition.png#center" >}}

En utilisant le pack d'animations 3D rajouté à notre projet, nous pouvons :

1. créer 3 états intitulés `Idle`, `Hit` et `Attack`;
2. leur associer les animations adéquates;
3. rajouter les transitions nécessaires pour passer de `Idle` à `Hit` (et vice-versa) et de `Idle` à `Attack`;
4. créer les {{<unity_keyword `Triggers` >}} `Hit` et `Attack` et les associer aux transitions adéquates.
En suivant ces étapes, ceci nous donne un graphe qui ressemble à ceci :
{{<figure src="images/UnityAnimatorControllerWithStates.png#center" >}}

### Les Blend Trees

Les {{<unity_keyword `Blend Trees` >}}[^4] permettent de combiner des {{<unity_keyword `Animation Clips` >}} en temps-réel afin de générer de nouvelles animations.
Par exemple, vous pouvez combiner une animation de marche lente avec une animation de marche rapide pour créer des animations de marche à des vitesses variables.

Les {{<unity_keyword `Blend Trees` >}} sont en fait contenus par certains états du graphe.
Ils englobent plusieurs {{<unity_keyword `Animation Clips` >}} et un système pour interpoler entre eux.
Il est possible de créer un état contenant un {{<unity_keyword `Blend Tree` >}} vide en faisant un clic droit dans la fenêtre {{<unity_window `Animator` >}} puis sélectionner {{<unity_menu `Create State > From New Blend Tree` >}} :
{{<figure src="images/UnityCreateStateWithBlendTree.png#center" >}}

Il est aussi possible de rajouter un {{<unity_keyword `Blend Tree` >}} dans un état existant en faisant un clic droit sur un état existant et en choisissant {{<unity_menu `Create new BlendTree in State` >}} :
{{<figure src="images/UnityAddBlendTreeInState.png#center" >}}

Si l'on crée un {{<unity_keyword `Blend Tree` >}} et qu'on l'ouvre en double-cliquant dessus, alors on obtient quelque chose comme ce qui suit dans l'{{<unity_window `Inspector` >}} :
{{<figure src="images/UnityBlendTree.png#center" >}}

Dans un premier temps, il est important de choisir la façon donc le {{<unity_keyword `Blend Tree` >}} va interpoler les animations entre elles.
Pour ceci, il existe plusieurs types d'interpolation :

- **1D[^5] :** les animations sont interpolées en 1 dimension, donc selon un paramètre unique;
- **2D Simple Directional[^6] :** les animations sont interpolées en 2 dimensions, donc en utilisant 2 paramètres.
Certaines restrictions (vitesses des animations, directions inférieures à 180°, etc.) peuvent limiter son utilisation;
- **2D Freeform Directional[^6] :** ce type d'interpolation est similaire à ce qui précède mais avec moins de contraintes.
Il est cependant plus compliqué à utiliser;
- **2D Freeform Cartesian[^6] :** ici l'interpolation n'est plus optimisée pour des animations de locomotion mais peut être utilisée pour interpoler toute sorte de mouvements.
- **Direct[^7] :** ce dernier type d'interpolation permet de gérer directement l'interpolation avec plusieurs paramètres.

Les {{<unity_keyword `Blend Trees` >}} demandent donc des paramètres en entrée pour calculer l'interpolation.
Ces paramètres sont rajoutés de manière identique aux {{<unity_keyword `Triggers` >}} vus précédemment.
Dans le cas d'un moteur d'animation de locomotion par exemple, on peut vouloir contrôler la vitesse et la direction de déplacement.
Dans ce cas, on peut créer des paramètres de type {{<unity_keyword `Float` >}}.
Enfin, dans l'{{<unity_window `Inspector` >}}, on rajoute ces paramètres comme entrées au {{<unity_keyword `Blend Tree` >}}.

À ce stade, il nous reste encore à rajouter des {{<unity_keyword `Animation Clips` >}}.
Pour ce faire, il faut aller dans la section {{<unity_keyword `Motion` >}} dans la fenêtre {{<unity_window `Inspector` >}}, cliquer sur le `+` et sélectionner {{<unity_menu `Add Motion Field` >}} :
{{<figure src="images/UnityAddMotionFieldToBlendTree.png#center" >}}

À chaque {{<unity_keyword `Motion Field` >}} ainsi créé, on va associer des valeurs des paramètres du {{<unity_keyword `Blend Tree` >}}.
Quand ces valeurs seront entrées dans le {{<unity_keyword `Blend Tree` >}}, alors l'{{<unity_keyword `Animation Clip` >}} sera jouer à 100%.
Sinon, le {{<unity_keyword `Blend Tree` >}} va prendre les mouvements les plus proches (en termes de valeurs des paramètres) et les interpoler.

Pour reprendre notre exemple, nous devons donc :

1. créer un {{<unity_keyword `Blend Tree` >}} dans l'état `Idle`;
2. rajouter 2 paramètres de type `Float` (appelés par exemple `Speed` et `Direction`) à notre {{<unity_keyword `Animator Controller` >}};
3. choisir le type {{<unity_keyword `2D Freeform Directional` >}} pour le paramètre {{<unity_keyword `Blend Type` >}};
4. rajouter 4 {{<unity_keyword `Motion Fields` >}} pour les {{<unity_keyword `Animation Clips` >}} souhaités dans le {{<unity_keyword `Blend Tree` >}} comme par exemple un mouvement `Idle`, `Move Forward`, `Move Left` et `Move Right`;
5. pour chaque {{<unity_keyword `Motion Field` >}}, spécifier les valeurs `(vitesse, direction)` qu'ils représentent.
Par exemple, pour le mouvement `Idle`, alors on peut lui donner les valeur `(0, 0)`.
Pour le mouvement `Move Forward` les valeurs `(1, 0)`.
Pour le mouvement `Move Left` les valeurs `(1, -1)` et enfin pour le mouvement `Move Right` les valeurs `(1, 1)`.

## Contrôler le moteur d'animations

Nous avons donc pour le moment un moteur d'animations 3D qui a plusieurs paramètres.
Il nous reste enfin à le modifier pour le faire réagir en temps-réel aux différents événements de notre application 3D.

Les transitions ont des conditions qui leur sont attachées.
Par exemple, la transition entre l'état `Idle` et l'état `Attack` va s'activer lorsque l'utilisateur active l'{{<unity_keyword `Axis` >}} nommé `Fire1`.
Pour ce faire, il suffit d'attacher le {{<unity_keyword `Script` >}} suivant au personnage 3D :
{{< highlight csharp "linenos=table" >}}
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Attack : MonoBehaviour
{
    private Animator m_animator;
    // Start is called before the first frame update
    void Start()
    {
        m_animator = GetComponent<Animator>();
    }

    // Update is called once per frame
    void Update()
    {
        if (Input.GetAxis("Fire1") > 0)
        {
            m_animator.SetTrigger("Attack");
        }
    }
}
{{< /highlight >}}

Enfin, on peut modifier les paramètres `Speed` et `Direction` quand l'utilisateur presse les touches associées aux {{<unity_keyword `Axis` >}} `Horizontal` et `Vertical` :
{{< highlight csharp "linenos=table" >}}
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class UserControls : MonoBehaviour
{
    private Animator m_animator;
    // Start is called before the first frame update
    void Start()
    {
        m_animator = GetComponent<Animator>();
    }

    // Update is called once per frame
    void Update()
    {
        if (Input.GetAxis("Fire1") > 0)
        {
            m_animator.SetTrigger("Attack");
        }

        float speed = Input.GetAxis("Vertical");
        if (speed != 0)
        {
            m_animator.SetFloat("Speed", speed);
        }
        float direction = Input.GetAxis("Horizontal");
        if (direction != 0)
        {
            m_animator.SetFloat("Direction", direction);
        }
    }
}
{{< /highlight >}}

## Slides

{{<slides "http://enseignement.pages.ing.he-arc.ch/isc/cours/niveau-3/3292.2-infographie-unity/slides/Chap4_Animation3D.html">}}

## Références
[^1]: [Animator Controllers, Unity](https://docs.unity3d.com/Manual/AnimatorControllers.html)
[^2]: [Animation Clips, Unity](https://docs.unity3d.com/Manual/AnimationClips.html)
[^3]: [State Machine Transitions, Unity](https://docs.unity3d.com/Manual/StateMachineTransitions.html)
[^4]: [Blend Trees, Unity](https://docs.unity3d.com/Manual/class-BlendTree.html)
[^5]: [1D Blending, Unity](https://docs.unity3d.com/Manual/BlendTree-1DBlending.html)
[^6]: [2D Blending, Unity](https://docs.unity3d.com/Manual/BlendTree-2DBlending.html)
[^7]: [Direct Blending, Unity](https://docs.unity3d.com/Manual/BlendTree-DirectBlending.html)
[^Mixamo]: [Mixamo](https://www.mixamo.com/)
