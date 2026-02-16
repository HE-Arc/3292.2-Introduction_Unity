---
title: Les Events dans Unity
author: "Benoit Le Callennec"
date: 2020-09-17
tags : [
    "Unity", "Scripting"
    ]
---
Il existe plusieurs types d'***Events*** utilisables dans Unity : les ***UnityEvents***[^1] et les ***Events*** C# natifs[^2]. Les **Events** offrent un moyen simple et efficace de construire un système de diffusion de messages.
Ils suivent essentiellement le design pattern ***Observer***[^3]^.

Le seul avantage à utiliser les ***UnityEvents*** c'est qu'ils sont intégrés directement dans l'éditeur[^4].
Cependant les ***UnityEvents*** sont beaucoup plus lents que les ***Events*** C# natifs[^5].
En conclusion, utilisez les ***Events*** C# natifs de préférence.

## À regarder (pour aller plus loin)
<center>
<iframe width="734" height="413" src="https://www.youtube.com/embed/videoseries?list=PLoMYgUbrKKtdrYp5bleaEwCw0og7eYNTm" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</center>

## Références
[^1]: [UnityEvents, Unity](https://docs.unity3d.com/Manual/UnityEvents.html)
[^2]: [Handling and raising events, Microsoft](https://docs.microsoft.com/en-us/dotnet/standard/events/)
[^3]: [Observer, Game Programming Patterns](https://gameprogrammingpatterns.com/observer.html)
[^4]: [Why choose UnityEvent over native C# events?, stackoverflow](https://stackoverflow.com/questions/44734580/why-choose-unityevent-over-native-c-sharp-events)
[^5]: [Event Performance: C# vs. UnityEvent, Jackson Dunstan](https://www.jacksondunstan.com/articles/3335)