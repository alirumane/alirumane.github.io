---
layout: post
title: Working with JSON Data in C
tags: [JSON, C]
category: [C]
thumbnail : images/post/thumbs/working-with-json-data-in-c.jpg
description: JSON with C
---

<p><i class="fa fa-quote-left fa-2x fa-pull-left fa-border"></i></p>

[JavaScript Object Notation](http://json.org/) aka JSON is a lightweight text based human readable data-interchange format following JavaScript object syntax. It is often considered as a replacement for XML in AJAX systems.


If you are working with some API or with an IoT device that pushes some data to an API, there is a possibility you might be using JSON for the exchange of request.

Is it a good practice to use JSON formatted data as an exchange for an IoT device that usually has the bandwidth, power, and processing as a constraint? Let's keep that topic for another day and focus on working with JSON data in C.


#### Table of Contents

1. [Brief](#brief)
1. [JSON Structure](#json-structure)
1. [Native C](#native-c)
1. [Library](#library)
	1. [Dependencies](#dependencies)
	1. [Building](#building)
1. [Finally!](#finally)

Let's take an example from [developer Mozilla site's JSON structure](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/JSON#JSON_structure) as a reference.

#### JSON Structure


JSON stores data in the form of name/key value pairs.

JSON should have either an object or an array at its root. It can be empty but either an object or an array should be present.

Following are the data types supported by JSON
- string: a sequence of characters between double quotes ("")
- number: digits with base 10, can be negative, fraction or exponent of 10
- boolean: true or false
- null/empty: value unassigned
- object: an unordered set of name-value pair between curly braces, can be empty or separated by comma (,) if multiple are used
- array : an ordered collection of values between square braces separated by a comma (,)


A simple valid JSON structure can be:

```javascript
{
}
```

or

```javascript
[
]
```


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


```c
#include <stdio.h> 
#include "cJSON.h"

int main()
{
  const char *const memberName[] = {"Molecule Man", "Madame Uppercut", "Eternal Flame", "Farari"};
  const int const memberAge[] = {29, 39, 1000000};
  const char *const memberSecIdentity[] = {"Dan Jukes", "Jane Wilson", "Unknown"};
  const char *const memberPower[][5] = {
      {"Radiation resistance", "Turning tiny", "Radiation blast"},
      {"Million tonne punch", "Damage resistance", "Superhuman reflexes"},
      {"Immortality", "Heat Immunity", "Inferno", "Teleportation", "Interdimensional travel"}};

  cJSON *root = cJSON_CreateObject();
  cJSON_AddStringToObject(root, "squadName", "Super hero squad");
  cJSON_AddStringToObject(root, "homeTown", "Metro City");
  cJSON_AddNumberToObject(root, "formed", 2016);
  cJSON_AddStringToObject(root, "secretBase", "Super tower");
  cJSON_AddStringToObject(root, "active", "true");

  cJSON *members = cJSON_CreateArray();
  for (size_t i = 0; i < 3; i++)
  {
    cJSON *member = cJSON_CreateObject();
    cJSON_AddItemToObject(member, "name", cJSON_CreateString(memberName[i]));
    cJSON_AddItemToObject(member, "age", cJSON_CreateNumber(memberAge[i]));
    cJSON_AddItemToObject(member, "secretIdentity", cJSON_CreateString(memberSecIdentity[i]));

    cJSON *powers = cJSON_CreateArray();
    for (int j = 0; j < 5; j++)
    {
      if (memberPower[i][j] != NULL)
      {
        cJSON_AddItemToArray(powers, cJSON_CreateString(memberPower[i][j]));
      }
    }
    cJSON_AddItemToObject(member, "powers", powers);
    cJSON_AddItemToArray(members, member);
  }
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
                        "powers":       ["Radiation resistance", "Turning tiny", "Radiation blast"]
                }, {
                        "name": "Madame Uppercut",
                        "age":  39,
                        "secretIdentity":       "Jane Wilson",
                        "powers":       ["Million tonne punch", "Damage resistance", "Superhuman reflexes"]
                }, {
                        "name": "Eternal Flame",
                        "age":  1000000,
                        "secretIdentity":       "Unknown",
                        "powers":       ["Immortality", "Heat Immunity", "Inferno", "Teleportation", "Interdimensional travel"]
                }]
}
```
