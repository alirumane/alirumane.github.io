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

JSON data is written as name/value pairs.


From  above example: name squadName value Super hero squad.


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
  return 0;
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

Json array


```c
int main()
{
  cJSON *root = cJSON_CreateObject();
  cJSON_AddStringToObject(root, "squadName", "Super hero squad");
  cJSON_AddStringToObject(root, "homeTown", "Metro City");
  cJSON_AddNumberToObject(root, "formed", 2016);
  cJSON_AddStringToObject(root, "secretBase", "Super tower");
  cJSON_AddStringToObject(root, "active", "true");

  cJSON *members = cJSON_CreateArray();
  cJSON *member = cJSON_CreateObject();
  cJSON_AddItemToObject(member, "name", cJSON_CreateString("Molecule Man"));
  cJSON_AddItemToObject(member, "age", cJSON_CreateNumber(29));
  cJSON_AddItemToObject(member, "secretIdentity", cJSON_CreateString("Dan Jukes"));
  cJSON_AddItemToArray(members, member);
  cJSON_AddItemToObject(root, "members", members);

  char *json = NULL;
  json = cJSON_Print(root);
  cJSON_Delete(root);
  printf("%s", json);
  return 0;
}
```

```javascript
{
        "squadName":    "Super hero squad",
        "homeTown":     "Metro City",
        "formed":       2016,
        "secretBase":   "Super tower",
        "active":       "true",
        "members":      [{
                        "name": "Molecule Man",
                        "age":  29,
                        "secretIdentity":       "Dan Jukes"
                }]
}
```

```c
int main()
{
  cJSON *root = cJSON_CreateObject();
  cJSON_AddStringToObject(root, "squadName", "Super hero squad");
  cJSON_AddStringToObject(root, "homeTown", "Metro City");
  cJSON_AddNumberToObject(root, "formed", 2016);
  cJSON_AddStringToObject(root, "secretBase", "Super tower");
  cJSON_AddStringToObject(root, "active", "true");

  cJSON *members = cJSON_CreateArray();
  cJSON *member = cJSON_CreateObject();
  cJSON_AddItemToObject(member, "name", cJSON_CreateString("Molecule Man"));
  cJSON_AddItemToObject(member, "age", cJSON_CreateNumber(29));
  cJSON_AddItemToObject(member, "secretIdentity", cJSON_CreateString("Dan Jukes"));

  cJSON *powers = cJSON_CreateArray();
  cJSON_AddItemToArray(powers, cJSON_CreateString("Radiation R"));
  cJSON_AddItemToArray(powers, cJSON_CreateString("Turning tiny"));
  cJSON_AddItemToArray(powers, cJSON_CreateString("Radiation blast"));
  cJSON_AddItemToObject(member, "powers", powers);

  cJSON_AddItemToArray(members, member);
  cJSON_AddItemToObject(root, "members", members);

  char *json = NULL;
  json = cJSON_Print(root);
  cJSON_Delete(root);
  printf("%s", json);
  return 0;
}
```


```javascript
{
        "squadName":    "Super hero squad",
        "homeTown":     "Metro City",
        "formed":       2016,
        "secretBase":   "Super tower",
        "active":       "true",
        "members":      [{
                        "name": "Molecule Man",
                        "age":  29,
                        "secretIdentity":       "Dan Jukes",
                        "powers":       ["Radiation R", "Turning tiny", "Radiation blast"]
                }]
}
```
