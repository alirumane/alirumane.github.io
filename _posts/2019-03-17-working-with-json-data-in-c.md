---
layout: post
title: Working with JSON Data in C
tags: [JSON, C]
category: [C]
thumbnail : images/post/thumbs/working-with-json-data-in-c.jpg
description: JSON with C
---

<p><i class="fa fa-quote-left fa-2x fa-pull-left fa-border"></i></p>

[JavaScript Object Notation](http://json.org/) aka JSON is a lightweight data-interchange format.


Let's take an example from [developer Mozilla site's JSON structure](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/JSON#JSON_structure) as a reference.

```javascript
{
  "squadName": "Super hero squad",
  "homeTown": "Metro City",
  "formed": 2016,
  "secretBase": "Super tower",
  "active": true,
  "members": [
    {
      "name": "Molecule Man",
      "age": 29,
      "secretIdentity": "Dan Jukes",
      "powers": [
        "Radiation resistance",
        "Turning tiny",
        "Radiation blast"
      ]
    },
    {
      "name": "Madame Uppercut",
      "age": 39,
      "secretIdentity": "Jane Wilson",
      "powers": [
        "Million tonne punch",
        "Damage resistance",
        "Superhuman reflexes"
      ]
    },
    {
      "name": "Eternal Flame",
      "age": 1000000,
      "secretIdentity": "Unknown",
      "powers": [
        "Immortality",
        "Heat Immunity",
        "Inferno",
        "Teleportation",
        "Interdimensional travel"
      ]
    }
  ]
}
```


We will use [cJSON](https://github.com/DaveGamble/cJSON) for parsing JSON data in C.


```c
#include <stdio.h> 
#include "cJSON.h"

int main()
{
  cJSON *root = cJSON_CreateObject();
  cJSON_AddStringToObject(root, "squadName", "Super hero squad");
  cJSON_AddStringToObject(root, "homeTown", "Metro City");
  cJSON_AddNumberToObject(root, "formed", 2016);
  cJSON_AddStringToObject(root, "secretBase", "Super tower");
  cJSON_AddStringToObject(root, "active", "true");

  char *json = NULL;
  json = cJSON_Print(root);
  cJSON_Delete(root);
  printf("%s", json);
}
```

Don't forget to use -lm while compiling the code.

```javascript
{
        "squadName":    "Super hero squad",
        "homeTown":     "Metro City",
        "formed":       2016,
        "secretBase":   "Super tower",
        "active":       "true"
}
```

