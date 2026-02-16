---
title: "Chapitre 3 : scripting"
---

# Chapitre 3 : scripting
Dans Unity, l'intelligence de l'application 3D se programme grâce à des scripts C#.
Lorsque ces scripts sont attachés à un {{<unity_keyword `GameObject` >}}, alors Unity les exécute en fonction des événements qui interviennent.

## Hello World
Pour attacher un script à un objet dans la scène 3D, il faut sélectionner le {{<unity_keyword `GameObject` >}} puis cliquer sur le bouton {{<unity_button `Add Component` >}}.
Ensuite, on renseigne le nom du script que l'on souhaite attacher.
La figure suivante résume ce que vous devriez obtenir :
{{<figure src="images/UnityScriptComponent.png#center" >}}

S'il n'est pas présent, alors il est automatiquement créé en cliquant sur {{<unity_button `New Script` >}} puis sur {{<unity_button `Create and Add` >}}.
Le script peut ensuite être ouvert dans votre IDE en double-cliquant dessus.
Il ressemble à ce qui suit :

{{< highlight csharp "linenos=table,hl_lines=8 14">}}
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class HelloWorld : MonoBehaviour
{
    // Start is called before the first frame update
    void Start()
    {
        
    }

    // Update is called once per frame
    void Update()
    {
        
    }
}
{{< / highlight >}}

Le script contient déjà 2 fonctions importantes : `void Start()` et `void Update()`.
Comme indiqué dans les commentaires : 
- `void Start()` est appelée **1 seule fois**, durant la frame où il est activé (en général au début de l'exécution);
- `void Update()` est appelée **à chaque frame**.

Il est très facile d'afficher un message à chaque appel à `void Start()` ainsi qu'à `void Update()`.
Pour cela, il suffit de modifier le script pour rajouter un appel à la fonction `Log()` de la classe `Debug`[^1] comme indiqué dans le code qui suit :

{{< highlight csharp "linenos=table, hl_lines=10 16">}}
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class HelloWorld : MonoBehaviour
{
    // Start is called before the first frame update
    void Start()
    {
        Debug.Log("Hello Start()");
    }

    // Update is called once per frame
    void Update()
    {
        Debug.Log("Hello Update()");
    }
}
{{< / highlight >}}

Lorsque l'on exécute l'application, on peut regarder ce qui est affiché dans la fenêtre {{<unity_window `Console` >}} :
{{<figure src="images/UnityHelloWorldConsole.png#center" >}}
En particulier, on remarque bien que le message `Hello Start()` est affiché une seul fois au début, et que le message `Hello Update()` est affiché en continu, comme attendu.

Comme vous l'avez sans doute déjà remarqué, un {{<unity_keyword `Script` >}} est en fait un {{<unity_keyword `Component` >}}.
Il doit donc être attaché à un {{<unity_keyword `GameObject` >}} pour être exécuté.
De plus, il faut noter que les membres publics d'un {{<unity_keyword `Script` >}} sont automatiquement accessibles depuis l'éditeur de Unity.
C'est très pratique lorsque l'on souhaite pouvoir modifier et tester rapidement des paramètres du script à l'exécution.
Enfin, il faut remarquer que le {{<unity_keyword `Script` >}} hérite de la classe `MonoBehavior`.
C'est la classe `MonoBehavior` qui gère en particulier le comportement général du {{<unity_keyword `Script` >}} (quand il est instancié, quelles fonctions sont appelées, quand elles sont appelées, etc.).

{{<hint danger >}}
**Constructor et Destructor**

Unity gère lui-même la création et la destruction des {{<unity_keyword `Scripts` >}}.
Il ne faut donc surtout pas implémenter les constructeurs au risque de perturber le fonctionnement complet de votre application.
{{</hint >}}

## Event Functions
Les {{<unity_keyword `Scripts` >}} ont des points d'entrées (des fonctions) prédéfinis qui vont être automatiquement appelés par Unity en réponse à certains événements : ce sont les {{<unity_keyword `Event Functions` >}}[^EventFunctions].

{{<hint info >}}
**Remarque**

les fonctions `void Start()` et `void Update()` sont des {{<unity_keyword `Event Functions` >}}.
{{</hint >}}

L'ordre d'exécution des {{<unity_keyword `Event Functions` >}} est important.
La figure suivante résume les principales {{<unity_keyword `Event Functions` >}} et surtout leur ordre d'exécution :
{{<figure src="images/UnityEventFunctionsExecOrder.png#center" >}}

Elles sont documentées dans la classe `MonoBehavior`[^2].
Il faut noter qu'elles sont très nombreuses et que seul un sous-ensemble d'entre elles est en général utilisé.

{{<hint info >}}
**Remarque**

On voit par exemple que toutes les fonctions `void Update()` exécutées avant les fonctions `void LateUpdate()`.
{{</hint >}}

{{<hint danger >}}
**ATTENTION**

L'ordre d'exécution des mêmes {{<unity_keyword `Event Functions` >}} (toutes les `void Update()` par exemple) n'est pas défini.
{{</hint >}}

## Time.DeltaTime
Il est important de garder à l'esprit que la fonction `void Update()` est appelée à chaque frame, c'est-à-dire aussi souvent que possible.
Par conséquent, elle ne tient pas compte du temps écoulé entre 2 frames rendues.
Ainsi, le résultat de la fonction `void Update()` peut dépendre du frame rate de votre application.
Par exemple, lorsqu'elle est chargée de déplacer un {{<unity_keyword `GameObject` >}} d'une certaine distance à chaque frame, alors :
- si le frame rate est élevé (par exemple sur une machine puissante), elle sera appelée très souvent. Le {{<unity_keyword `GameObject` >}} se déplacera donc très vite.
- Au contraire, si le frame rate est faible, elle sera appelée moins souvent. Le {{<unity_keyword `GameObject` >}} se déplacera dans ce cas plus lentement.

En général, avoir une application 3D dont le comportement dépend de la machine sur laquelle elle est exécutée n'est pas souhaitable.
Pour corriger ce problème, il faut utiliser `Time.DeltaTime` qui nous renseigne sur le temps écoulé depuis le dernier appel à `void Update()`.
Ainsi, il est facile de rendre l'exécution de cette fonction indépendante du frame rate :
{{< highlight csharp "linenos=table, hl_lines=4">}}
public float speed = 5;
void Update()
{
  float distance = speed * Time.deltaTime;
  transform.Translate(Vector3.up * distance);
}
{{< / highlight >}}

<!--- there is a bug when including shortcodes in headers. So we must use the alternative syntax. -->
## Modifier des {{%unity_keyword `GameObjects` %}} à l'exécution
Un script peut modifier les {{<unity_keyword `Components` >}} :
1. appartenant au même {{<unity_keyword `GameObject` >}} (celui auquel il est attaché);
2. appartenant à d'autres {{<unity_keyword `GameObjects` >}} qu'il connaît au préalable;
3. appartenant à d'autres {{<unity_keyword `GameObjects` >}} qui sont instanciés (et détruits) dynamiquement.

<!--- there is a bug when including shortcodes in headers. So we must use the alternative syntax. -->
### Modifier les {{%unity_keyword `Components` %}} du même {{%unity_keyword `GameObject` %}}
Un {{<unity_keyword `Script` >}} a accès aux {{<unity_keyword `Components` >}} attachés au même {{<unity_keyword `GameObject` >}} en utilisant leur type :
{{< highlight csharp >}}
public Component GetComponent<Type>();
{{< / highlight >}}
Ou plus rarement :
{{< highlight csharp >}}
public Component[] GetComponents<Type>();
{{< /highlight >}}
Par exemple, pour récupérer le {{<unity_keyword `RigidBody` >}} attaché au même {{<unity_keyword `GameObject` >}} que le {{<unity_keyword `Script` >}}, on peut faire :
{{< highlight csharp "linenos=table,hl_lines=1">}}
var rigidBody = GetComponent<Rigidbody>();
rigidBody.AddForce(new Vector3(0, 500, 0));
rigidBody.AddTorque(new Vector3(30, 30, 30));
{{< /highlight >}}

<!--- there is a bug when including shortcodes in headers. So we must use the alternative syntax. -->
### Modifier les {{%unity_keyword `Components` %}} d'autres {{%unity_keyword `GameObjects` %}} connus
Il est possible pour un {{<unity_keyword `Script` >}} de modifier des {{<unity_keyword `Components` >}} appartenant à d'autres {{<unity_keyword `GameObjects` >}}.
En particulier, si le {{<unity_keyword `GameObject` >}} est connu au préalable, et si le lien entre le {{<unity_keyword `Script` >}} et le {{<unity_keyword `GameObject` >}} (ou le {{<unity_keyword `Component` >}}) à interroger ou modifier est permanent, alors on peut tout simplement rajouter un membre public dans le {{<unity_keyword `Script` >}} (le {{<unity_keyword `GameObject`>}} ou directement le {{<unity_keyword `Component` >}} que l'on attend) :
{{< highlight csharp "linenos=table,hl_lines=3 4">}}
public class CheckProximityObserver : MonoBehaviour
{
    public GameObject go1;
    public GameObject go2;

    ...
}
{{< /highlight >}}

Comme les membres sont publics, alors ils sont directement visibles dans l'éditeur.
Il suffit donc de faire un drag-and-drop des {{<unity_keyword `GameObjects` >}} que l'on souhaite utiliser :
{{<figure src="images/UnityGOAsPublicMember.png#center" >}}

Ensuite, dans le {{<unity_keyword `Script` >}}, on peut tout simplement utiliser les {{<unity_keyword `GameObjects` >}} (ou les {{<unity_keyword `Components` >}}) liés de la manière suivante :
{{< highlight csharp "linenos=table,hl_lines=3 4 9 11 16 18">}}
    void Update()
    {
        var pos1 = go1.transform.position;
        var pos2 = go2.transform.position;
        var distance = pos2 - pos1;

        if (distance.magnitude < maxDistance)
        {
            var m1 = go1.GetComponent<Renderer>().material;
            m1.color = new Color(1, 0, 0);
            var m2 = go2.GetComponent<Renderer>().material;
            m2.color = new Color(1, 0, 0);
        }
        else
        {
            var m1 = go1.GetComponent<Renderer>().material;
            m1.color = new Color(0, 0, 1);
            var m2 = go2.GetComponent<Renderer>().material;
            m2.color = new Color(0, 0, 1);
        }
    }
{{< /highlight >}}

<!--- There is a bug when including shortcodes in headers. So we must use the alternative syntax. -->
### Modifier les {{%unity_keyword `Components` %}} d'autres {{%unity_keyword `GameObjects` %}} créés dynamiquement
Si les {{<unity_keyword `GameObjects` >}} sont créés et détruits dynamiquement, alors il est préférable de tous les grouper en les parentant au même {{<unity_keyword `GameObject` >}}.
Ce dernier va donc servir de conteneur, que l'on passe au script en utilisant un membre public.
Il ne reste plus qu'à itérer sur tous les {{<unity_keyword `Components` >}} du conteneur ayant le type désiré :
{{< highlight csharp "linenos=table,hl_lines=3 8 16">}}
public class CheckProximityObserver2 : MonoBehaviour
{
    public Transform chairs;
    public float maxDistance;
    void Update()
    {
        // Iterate over all Transforms (children) contained in chairs group
        foreach (Transform t1 in chairs)
        {
            string name = transform.name;

            // First reset its color to ok
            var mat = t1.GetComponent<Renderer>().material;
            mat.color = new Color(0, 1, 0);

            foreach (Transform t2 in chairs)
            {
                if (t1 == t2)
                {
                    continue;
                }

                var currentDistance = (t1.position - t2.position).magnitude;
                if (currentDistance < maxDistance)
                {
                    // Then set color to error
                    mat.color = new Color(1, 0, 0);

                    break;
                }
            }
        }
    }
}
{{< /highlight >}}

{{<hint danger >}}
**ATTENTION**

Les méthodes **`GetComponent<Type>()`** et **`GetComponents<Type>()`** sont coûteuses en temps de calcul.
Il faut donc éviter de les appeler trop souvent à l'exécution.
En particulier, dans les exemples précédents, il est préférable de les appeler une seule fois dans la fonction **`void Start()`** et de stocker le résultat dans une variable membre.
{{</hint >}}

## Recherche de {{%unity_keyword `GameObjects` %}} à l'exécution
Il est possible de rechercher des {{<unity_keyword `GameObjects` >}} à l'exécution en utilisant leur nom ou leur tag grâce au fonctions suivantes :
{{< highlight csharp >}}
public static GameObject Find(string name);
public static GameObject FindWithTag(string tag);
public static GameObject[] FindGameObjectsWithTag(string tag);
{{< /highlight >}}
Par exemple, il est possible de récupérer tous les {{<unity_keyword `GameObjects` >}} qui ont comme `Tag` "Cubes" :
{{< highlight csharp "linenos=table,hl_lines=3 5">}}
var GOs = GameObject.Find("Cube");

var firstCube = GameObject.FindWithTag("Cubes");

var allCubes = GameObject.FindGameObjectsWithTag("Cubes");
foreach(GameObject go in allCubes)
{
    // Do great things here
}
{{< /highlight >}}

## Instancier et détruire des {{%unity_keyword `GameObjects` %}} à l'exécution
Pour instancier des {{<unity_keyword `GameObjects` >}} à l'exécution, il faut utiliser la méthode `Instantiate`[^3] :
{{< highlight csharp >}}
public static Object Instantiate(Object original);
public static Object Instantiate(Object original, Transform parent);
public static Object Instantiate(Object original, Transform parent, bool instantiateInWorldSpace);
public static Object Instantiate(Object original, Vector3 position, Quaternion rotation);
public static Object Instantiate(Object original, Vector3 position, Quaternion rotation, Transform parent);
{{< /highlight >}}
L'objet `original` est souvent un {{<unity_keyword `Prefab` >}} passé en paramètre du script.

Pour détruire des {{<unity_keyword `GameObjects` >}} à l'exécution, il faut utiliser la méthode `Destroy`[^4] :
{{< highlight csharp >}}
public static void Destroy(Object obj, float t = 0.0F);
{{< /highlight >}}

## User Inputs
Pour une application 3D interactive, il est important de pouvoir écouter et récupérer les entrées de l'utilisateur.
Dans Unity, ces entrées sont configurables en allant dans le menu {{<unity_menu `Edit > Projects Settings` >}} :
{{<figure src="images/UnityEditProjectSettings.png#center" >}}
En sélectionnant `Input Manager`, vous obtenez une fenêtre similaire à celle montrée dans la figure suivante :
{{<figure src="images/UnityInputManagerWindow.png#center" >}}

Dans votre {{<unity_keyword `Script` >}}, il est ensuite facile de vérifier si l'utilisateur est en train de "se déplacer", en interrogeant l'état de l'`Axis` comme dans le code qui suit :
{{< highlight csharp "linenos=table,hl_lines=4" >}}
public float speed = 1.0f;
  void Update()
  {
    float hdisplacement = Input.GetAxis("Horizontal");
    var displacement = new Vector3(hdisplacement, 0, 0);
    displacement *= speed * Time.deltaTime;
    // DOES NOT WORK
    // transform.position.x += displacement.x;
    // OK
    // transform.position += displacement;
    // OK
    transform.Translate(displacement);
  }
{{< /highlight >}}

## Coroutines
Les {{<unity_keyword `Event Functions` >}} dans les {{<unity_keyword `Scripts` >}} sont synchrones : elles vont bloquer l'application le temps qu'elles s'exécutent.
On peut rendre certaines fonctions non-bloquantes en utilisant des {{<unity_keyword `Coroutines` >}}[^5].
C'est utile par exemple :
- pour répartir de **longs calculs** sur plusieurs frames;
- pour simuler un timer qui va exécuter une action après un certain délai.

Pour séparer les longs calculs sur plusieurs frames par exemple, il faut :
1. définir une {{<unity_keyword `Coroutine` >}}. Ceci se fait en définissant une méthode qui retourne un objet de type `IEnumerator`;
2. dans la {{<unity_keyword `Coroutine` >}}, rajouter un point de synchronisation avec Unity pour lui rendre la main jusqu'à la prochaine frame. Ceci se fait en utilisant le mot-clef `yield`;
3. enfin, il faut démarrer la {{<unity_keyword `Coroutine` >}}.
Ces 3 étapes sont résumées dans le code qui suit :
{{< highlight csharp "linenos=table,hl_lines=3 6 11" >}}
void Start()
{
  StartCoroutine("LongProcess");
}

IEnumerator LongProcess()
{
  for (int i = 0; i < 100; ++i)
  {
    Debug.Log(gameObject.name + ": Iteration #" + i);
    yield return null;
  }
}
{{< /highlight >}}

On peut aussi créer un timer avec un délai en utilisant la même technique, mais cette fois-ci dans le `yield`, on retourne un objet de type `WaitForSeconds` qui va suspendre l'exécution de la méthode pour un certain nombre de secondes.
Par exemple, si on souhaite faire "exploser" un {{<unity_keyword `GameObject` >}} un certain nombre de secondes après que l'utilisateur a appuyer sur la touche du haut, alors on pourrait faire comme ce qui suit :
{{< highlight csharp "linenos=table,hl_lines=4 7 11 13" >}}
private bool triggered = false;
void Update()
{
  if (Input.GetAxis("Vertical") > 0.0 && triggered == false)
  {
    triggered = true;
    StartCoroutine("Explode");
  }
}

IEnumerator Explode()
{
 yield return new WaitForSeconds(3.0f);
 var rigidBody = GetComponent<Rigidbody>();
 float fx = Random.Range(-500.0f, 500.0f);
 float fy = Random.Range(-500.0f, 500.0f);
 float fz = Random.Range(-500.0f, 500.0f);
 rigidBody.AddForce(new Vector3(fx, fy, fz));
 float tx = Random.Range(-50.0f, 50.0f);
 float ty = Random.Range(-50.0f, 50.0f);
 float tz = Random.Range(-50.0f, 50.0f);
 rigidBody.AddTorque(new Vector3(tx, ty, tz));
 triggered = false;
}
{{< /highlight >}}

Comme vu ci-dessus, il est possible de démarrer une coroutine en passant son nom sous forme de {{<unity_keyword `string` >}} à la méthode {{<unity_keyword `StartCoroutine` >}}.
Cette façon de faire à l'avantage d'être simple et suffit dans la grande majorité des cas.
Cependant, elle présente 2 désavantages majeurs :

- Elle est plus coûteuse en temps d'exécution.
- On ne peut passer qu'un seul paramètre à la {{<unity_keyword `Coroutine` >}}.

La 2ème approche consiste à passer directement la {{<unity_keyword `Coroutine` >}} avec ses paramètres au moment d'appeler {{<unity_keyword `StartCoroutine` >}}.

Enfin, il est possible d'arrêter une {{<unity_keyword `Coroutine` >}} avec la méthode {{<unity_keyword `StopCoroutine` >}}[^UnityDocStopCoroutine].

L'exemple suivant montre comment démarrer et arrêter une {{<unity_keyword `Coroutine` >}} à la demande.
Il montre aussi comment passer 2 (ou plus) paramètres à une {{<unity_keyword `Coroutine` >}} :
{{< highlight csharp "linenos=table,hl_lines=13 23 30" >}}
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Coroutine_101 : MonoBehaviour
{
    public string message = "";
    public float delay = 0.0f;

    [SerializeField]
    private bool running = false;

    private IEnumerator myCoroutine;

    void Start()
    {
    }

    void Update()
    {
        if (Input.GetAxis("Vertical") > 0.0 && running == false)
        {
            myCoroutine = MyCoroutine(message, delay);
            StartCoroutine(myCoroutine);
            running = true;
        }

        if (Input.GetAxis("Vertical") < 0.0)
        {
            StopCoroutine(myCoroutine);
            running = false;
        }
    }

    public IEnumerator MyCoroutine(string message, float delay)
    {
        int nbIterations = 0;
        while(true)
        {
            yield return new WaitForSeconds(delay);
            Debug.Log("MyCoroutine #" + nbIterations + "\nmessage: " + message + "\ndelay: " + delay);
            nbIterations++;
        }
    }
}{{< /highlight >}}

{{<hint info>}}
**Remarque**

Il faut noter qu'ici, on stocke le {{<unity_keyword `IEnumerator` >}} retourner par la {{<unity_keyword `Coroutine` >}} avant de la démarrer.
C'est nécessaire pour pouvoir l'arrêter par la suite.
Il est aussi possible d'appeler {{<unity_keyword `StopCoroutine` >}} en passant le nom de la {{<unity_keyword `Coroutine` >}} sous forme de {{<unity_keyword `string` >}}.
{{</hint >}}

## Slides

{{<slides "http://enseignement.pages.ing.he-arc.ch/isc/cours/niveau-3/3292.2-infographie-unity/slides/Chap3_Scripting.html#/">}}

## Références

[^1]: [Debug.Log, Unity](https://docs.unity3d.com/ScriptReference/Debug.Log.html)
[^2]: [MonoBehavior, Unity](https://docs.unity3d.com/ScriptReference/MonoBehaviour.html)
[^EventFunctions]: [Event Functions, Unity](https://docs.unity3d.com/Manual/EventFunctions.html)
[^EventFunctionsCallsSeq]:[Order of execution for event functions, Unity](https://docs.unity3d.com/Manual/ExecutionOrder.html)
[^3]: [Object.Instantiate, Unity](https://docs.unity3d.com/ScriptReference/Object.Instantiate.html)
[^4]: [Object.Destroy, Unity](https://docs.unity3d.com/ScriptReference/Object.Destroy.html)
[^5]: [Coroutines, Unity](https://docs.unity3d.com/Manual/Coroutines.html)
[^UnityDocStopCoroutine]: [StopCoroutine, Unity](https://docs.unity3d.com/ScriptReference/MonoBehaviour.StopCoroutine.html)
