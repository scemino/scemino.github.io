---
title: "Return to Monkey Island"
date: 2026-04-12T17:37:16+02:00
toc: true
draft: true
images:
tags:
  - rtmi
---

## Introduction

As a fan of the Monkey Island 1 and 2 adventure games since my early childhood, these games are among those I will never forget.
I was particularly happy to learn that Ron Gilbert was about to release "Return to Monkey Island".

![walkboxes1.png](/assets/images/rtmi.jpg)

## 2022 The First Experiments

And naturally, after working on `Thimbleweed Park` for several years, I was naturally curious to find out how the game worked.

I quickly discovered tools that let me list the contents of Weird.ggpack* resource files
Listing these files reveals a lot about the game engine, especially since some of them were already familiar to me—files with the extensions .ggpack, .tsv, .txt, .json, .wimpy, .lip, .png, and .yack were already used in `Thimbleweed...

Just look for these unfamiliar file extensions: .atlas, .ktxbz, .attach, .anim, .blend, .emitter, .ttf, .otf, .bank, .dink, .dinky.

I'm already familiar with the .ttf and .otf file extensions, which are the most common font file formats, so I won't go into detail about them.

As for the `Defines.dinky` file, it’s pretty easy to understand what it’s for since you can view its contents directly in a text editor. Plus, if you’ve been following the development of [Delores](https://github.com/grumpygamer/DeloresDev), you should already be familiar with the .dinky format.

After doing a little research, I discovered that .atlas, .attach, .anim, and .blend files are formats used by the [Spine 2D](https://esotericsoftware.com/) solution. I hadn’t heard of it before, and now I know where these beautiful animations come from—this solution is truly fantastic. Check out the [demos](https://esotericsoftware.com/spine-demos).

As for the .emitter files—given their name—I haven’t looked into them yet, but I might look into them later.

.bank files are used by the well-known audio solution [fmod](https://www.fmod.com/).

That leaves only the .ktxbz files.
Using the `file` command, we quickly get a clue as to their contents:

```sh
file BarDrinking-hd.ktxbz
BarDrinking-hd.ktxbz: zlib compressed data
```