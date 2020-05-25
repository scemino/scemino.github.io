---
layout: post
title:  "Savegames"
---

Aaah savegames... Without them it's impossible to go through the whole game.
In this post I will explain the internal format and the data used in these savegames.
<!--more-->

![savegames.png](/assets/img/savegames.png)

## The format

This format can be represented by a json struture, here is an example, a lot of data have been removed to make it clear:

```json
{
  "actors": {
    "bankmanager": {
      "_costume": "BankMgrAnimation",
      "_dir": 2,
      "_lockFacing": 0,
      "_pos": "{541,61}",
      "_roomKey": "Bank",
      "defaultVerb": 3,
      "detective": 0,
      "dialog": null,
      // ...
    },
  },
  "callbacks": {
    "callbacks": [
      {
        "function": "analyticsCallback",
        "guid": 8000217,
        "time": 29920
      }
    ],
    "nextGuid": 8000218
  },
  "currentRoom": "TrailerAlley",
  "dialog": {
    "#ChetAgentStreetDialog14reyes": 2,
    // ...
  },
    "easy_mode": 0,
  "gameGUID": "",
  "gameScene": {
    "actorsSelectable": 1,
    "actorsTempUnselectable": 0,
    "forceTalkieText": 0,
    "selectableActors": [
      {
        "_actorKey": "ray",
        "selectable": 1
      },
      // ...
    ]
  },
  "gameTime": 29738,
  "globals": {
    "abducted_agent": {
      "_actorKey": "ray"
    },
    "abducted_agent_seen": 1,
    "act1": 0,
    // ...
      },
  "inputState": 101,
  "inventory": {
    "slots": [
      {
        "jiggle": [
          1,
          0,
          0,
          0,
          0,
          0,
          0,
          0
        ],
        "objects": [
          "raysBadge",
          "raysNotebook",
          "countyMap1",
          "cellPhone",
          "fingerprintKit",
          "speckOfDustRay",
          "rayHotelKeycard",
          "pillowTronTool"
        ],
        "scroll": 0
      },
      // ...
    ]
  },
  "objects": {
    "aStreetArcadeDoorWF": {
      "flags": 1073742912,
      "name": "@29000"
    },
  },
  "rooms": {
    "AStreet": {
      "background": "AStreet",
      "speck_of_dust": 1,
      "speck_of_dust_collected": 1
    },
  },
  "savebuild": 0,
  "savetime": 1587988116,
  "selectedActor": "ransome",
  "version": 2
}
```

### Actors

For each actor the properties are saved, there are 2 types of properties:
* internal properties: costume, direction, position, they starts with an underscore
* script properties: defaultVerb, detective, dialog

### Callbacks

Callbacks are functions that can be called at a certain time of the game.
These callbacks are added from a script file, for example:
```squirrel
addCallback(60*5, analyticsCallback)
```

With this example:
```json
"callbacks": {
  "callbacks": [
    {
      "function": "analyticsCallback",
      "guid": 8000217,
      "time": 29920
    }
  ],
  "nextGuid": 8000218
},
```
* function: name of the function to call when time is elapsed
* guid: unique identifier of the callback
* time: time in ms to wait before calling the callback
* nextGuid: specify the identifier to use for the next callback

### Dialogs

As you know, we have to save the state of the dialogs in order to know what choices have been displayed or chosen.

This state is described like this:
```json
"dialog": {
    "#ChetAgentStreetDialog14reyes": 2,
    // ...
  },
```

Each line corresponds to a condition of a dialog, the format can be described like this:
`"[mode][dialog_name][line_number][actor]": [value]`

* mode: mode is one of the following value:
?: once
#: showonce
&: onceever
$: showonceever
^: temponce

* dialog_name: name of the dialog file without extension
* line_number: line number where the condition has been met in the dialog file
* actor: actor's key indicating which actor is used in this dialog
* value: don't know yet :(
