---
layout: single
title:  "Walkboxes & Pathfinding"
---

## Pathfinding

These days (huh these months), I worked a lot of time on fixing my pathfinding in engge.
First I have to explain what is pathfinding and walkboxes.
<!--more-->

## Walkboxes

What is a walkbox ? A walbox is a polygon where an actor (a character of the game) is able to walk.
For example, in this video, you can see that Delores follows the path to the vista and she is restricted to this path, it's not possible to walk on the grass.

{% include video id="z23CeNXuSf0" provider="youtube" %}

## How a walkbox is defined

In Thimbleweed Park walkboxes are defined in a file with the **wimpy** extension, for example in the previous video, the walkboxes are defined in a file named _QuickiePalOutside.wimpy_, like this:

```json
"walkboxes": [
    {
      "polygon": "{91,113};{173,113};{186,104};{329,104};{331,109};{412,109};{416,102};{494,102};{506,97};{532,94};{554,90};{660,66};{7,70};{8,86};{25,90};{19,104}"
    },
    {
      "polygon": "{730,114};{732,109};{554,90};{532,94}"
    },
    // etc.
  ]
```

This part is easy to understand, each walkbox is composed by a polygon, and each polygon is a set of points (x,y).

With engge, you can display these walkboxes with the debug tools:

![walkboxes1.png](/assets/images/walkboxes1.png)

OK now we have several polygons, what's next ?
Pathfinding of course.

## Pathfinding

> **Pathfinding** or **pathing** is the plotting, by a computer application, of the shortest route between two points. It is a more practical variant on solving mazes. This field of research is based heavily on Dijkstra's algorithm for finding the shortest path on a weighted graph.
(source: [wikipedia](https://en.wikipedia.org/wiki/Pathfinding))

Here comes the tricky part, to acheive this I read a lot blogs and documentations, and here is a list of useful resources:

* [Thimbleweed Park blog](https://blog.thimbleweedpark.com/walkbox_video)
* [http://www.groebelsloot.com/2016/03/13/pathfinding-part-2/](http://www.groebelsloot.com/2016/03/13/pathfinding-part-2/)
* [https://www.david-gouveia.com/pathfinding-on-a-2d-polygonal-map](https://www.david-gouveia.com/pathfinding-on-a-2d-polygonal-map)

With this great help, the actor is able to move inside a concave polygon, that's great... **but** we don't have a big polygon, we have several adjacent polygons.

After a long time, I found a magic library called [Clipper](https://sourceforge.net/projects/polyclipping/), this library can do a lot of things, but what I was looking for was a solution to merge several adjacent polygons.

And here is the result:
![walkboxes2.png](/assets/images/walkboxes2.png)

Not bad isn't it ?

You can even see the pathfinding in action, I converted the code (described in http://www.groebelsloot.com/2016/03/13/pathfinding-part-2/) from Haxe to C++ and I use the link [A star](https://en.wikipedia.org/wiki/A*_search_algorithm) algorithm.

{% include video id="ZoqC6v12HqY" provider="youtube" %}
