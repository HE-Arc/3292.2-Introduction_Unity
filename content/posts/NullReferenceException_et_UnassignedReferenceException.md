---
title: Null Reference Exception et Unassigned Reference Exception
author: "Benoit Le Callennec"
date: 2020-09-21
tags : [
    "Unity",
    "Scripting"
]
---
Dans Unity, quand vous accédez à une variable mal initialisée (ou pas initialisée du tout), vous récupérez une `NullReferenceException`[^1] ou une `UnassignedReferenceException`.
Ces erreurs apparaissent dans la console de la façon suivante :
{{<figure src="images/UnityConsoleError.png#center" width=100% >}}

Les erreurs les plus fréquentes sont :
- utiliser une variable exposée dans l'***Inspector*** mais non-assignée. Un simple ***drag and drop*** dans l'éditeur Unity suffit;
- utiliser une variable non-initialisée (contenant une référence nulle);
- mal épeler le nom d'un ***GameObject*** quand on utilise la fonction ***GameObject.Find()***[^2];
- le ***Variable Shadowing***[^3].

Le code suivant montre certaines de ces erreurs :
{{< highlight cs "linenos=table" >}}
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class ExceptionsExample : MonoBehaviour
{
	public GameObject unassignedRef1;
	[SerializeField] private GameObject unassignedRef2;
	private GameObject nullRef1;
	private GameObject nullRef2;
	private GameObject nullRef3;

	// Start is called before the first frame update
	private void Start()
	{
		// #1: not assigned in inspector
		Debug.Log(unassignedRef1.name);
		// #2: not assigned in inspector
		Debug.Log(unassignedRef2.name);
		// #3: not initialized
		Debug.Log(nullRef1.name);
		// #4: typo so Find() returns null
		var nullRef2 = GameObject.Find("exceptionCubeWithTypo");
		Debug.Log(nullRef2.name);
		// #5: shadowing, so ok here, but not ok in Shadowing()
		nullRef3 = gameObject;
		Debug.Log(nullRef3.name);
		Shadowing();
	}

	private void Shadowing()
    {
		// #5: shadowing
		GameObject nullRef3 = gameObject;
		Debug.Log(nullRef3.name);
	}
}
{{< / highlight >}}

## À regarder (pour aller plus loin)
{{< youtube id="5irv30-bTJw" >}}

## Références
[^1]: [Null Reference Exceptions, Unity](https://docs.unity3d.com/Manual/NullReferenceException.html)
[^2]: [GameObject.Find, Unity](https://docs.unity3d.com/ScriptReference/GameObject.Find.html)
[^3]: [Variable shadowing, Wikipedia](https://en.wikipedia.org/wiki/Variable_shadowing)
