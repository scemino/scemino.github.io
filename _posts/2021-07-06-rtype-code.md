---
layout: single
title:  "Let's make a shoot-em-up! (Part II)"
tags: tutorials R-Type shmup C++ lua
---

After designing the level in the [first part](2021-05-21-r-type.md), let's go to the exciting world of coding.
<!--more-->

---

First I want to share my evil plan to accomplish my goal:
- use an ECS [(Entity Component System)](https://en.wikipedia.org/wiki/Entity_component_system)
- be able to script with LUA
- define all animations in JSON 
- hot reload the game: textures/music/sounds/scripts and so on
- do the minimum of code in C++

---

## Why use an ECS ?

Well, this is something I wanted to try for a longtime, I like the principle to have a simple entity which can be extended with no limit without refactoring all my code.

## Use LUA scripting

I played with engge with Squirrel, but I wanted to try LUA for 2 reasons:
- LUA is used a lot in games
- the C++ bindings are really nice

## Animations defined in JSON

From my point of view, it's not interesting when you define the game logic, to have the animations defined in code. So this is my decision to seperate it and to create JSON files. About JSON, I found it enough human readable and easy to manipulate.

## Hot reloading

Recompiling and launching the game is a long process.
When you are designing your game, UI, enemy AI and so on you have start this process again and again, with scripting it's so easy to modify the code and restart the engine without restarting the executable.

## Minimum code in C++

If I want to use hot reloading I need to minimize the C++ code. If I'm able to code almost all the game logic in LUA, then it will be easier to use hit reloading.
So the question I need to ask myself anytime I add code in C++ is: can I do it in LUA instead ?
