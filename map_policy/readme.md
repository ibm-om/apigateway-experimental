---

copyright:
years: 2017
lastupdated: "2017-07-10"
author: "Om Goeckermann"
comment: "US Government Users Restricted Rights - Use, duplication, or
disclosure restricted by GSA ADP Schedule Contract with IBM Corp."
---
## Working with the map policy

### Tutorial


### Limitations

If you are familiar with API Connect version 5.x, you might notice some differences with how the Toolkit_preview **map** policy functions.
---
The new **map** policy provides location information and also supports multiple values for parameters. Consider the following.
```
v5:
    { 'request': { 'parameters': { 'foo': 123 } } }

Toolkit_preview:
    { 'request': { 'parameters': { 'foo': { 'locations': [ 'path' ], 'values': [123] } } } }
```
 The parameter `$(request.parameters.foo)` is substituted with `{ 'locations': [ 'path' ], 'values': [123] }`.
---
Objects with a period (.) in the name require the period to be escaped with \ for the **set**, **create**, **from** and **foreach** data specifications.
```
{"a.b.c" : { "d": "hello world" }}

        actions:
        - set: output.d\.e\.f.g
          from: input.a\.b\.c.d

{"d.e.f" : { "g": "hello world" }}
 ```


Toolkit-preview does not require map policy javascript to have strings escaped in the same manner as version 5. The following is valid swagger and the map policy in v6 writes the swagger in this manner, unlike the v5 map policy that insists on having the escaped string.

             - set: output.full_name
               from:
                 - input_string_1
                 - input_string_2
                value: |
                  var retValue = undefined;
                  if ($(input_string_1) !== undefined && $(input_string_2) !== undefined) {
                    retValue = $(input_string_1).toUpperCase() + ' ' + $(input_string_2).toUpperCase()"
                  }
                  retValue;
             - set: output.total_balance    # setting an output variable from multiple input numbers sums the numbers using the value field that is specified
               from:
                 - input_integer_1
                 - input_integer_2
               value:  |
                 var i1 = 0;
                 var i2 = 0;
                 if ($(input_integer_1) !== undefined) i1 = $(input_integer_1);
                 if ($(input_integer_2) !== undefined) i2 = $(input_integer_2);
                 i1 + i2;
