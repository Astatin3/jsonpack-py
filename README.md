A compression algorithm for JSON, converted to Python

## Notes

This is a copy of https://github.com/rgcl/jsonpack converted to python   
I have used this regularly in python 3.11, and haven't noticed any issues   
I have also removed the parameters from the functions entirely, because I was not able to get them to work   
There is also no package for this, unlike the original

## Introduction

jsonpack is a JavaScript program to pack and unpack JSON data.

It can compress to 55% of original size if the data has a recursive structure, example 
[Earthquake GeoJSON](http://earthquake.usgs.gov/earthquakes/feed/geojson/2.5/month) or 
[Twitter API](http://search.twitter.com/search.json?q=Twitter%20API&result_type=mixed). 

Install via:
> $ pip install jsonpackpy

### jsonpack.pack(json)
Retrieve a packed representation of the json

** Parameters **

* json {Object|string}: A valid JSON Object or their string representation

** Returns:** 

* string: the packed string representation of the data


#### Example

```python
import jsonpackpy as jpy

json = {
 	'type': 'world',
 	'name': 'earth',
 	'children': [{
 		'type': 'continent',
 		'name': 'America',
 		'children': [{
 			'type': 'country',
 			'name': 'Chile',
 			'children': [{
 				'type': 'commune',
 				'name': 'Antofagasta'
 			}]
 		}]
 	}, {
 		'type': 'continent',
 		'name' : 'Europe'
 	}]
 };
 	
 packed = jpy.pack(json)
 
 print(packed)
 # print:
 # "type|world|name|earth|children|continent|America|country|Chile|commune|Antofagasta|Europe^^^$0|1|2|3|4|@$0|5|2|6|4|@$0|7|2|8|4|@$0|9|2|A]]]]]|$0|5|2|B]]]"

```

### jsonpack.unpack(packed)

Unpack the data in the *packed* parameter

** Parameters **

* packed {string} : The result of call jsonpack.packed(...)

** Return: ** Object, the clone of the original JSON

#### Example

* Example 3: Browser

```python
import jsonpackpy as jpy

packed = "type|world|name|earth|children|continent|America|country|Chile|commune|Antofagasta|Europe^^^$0|1|2|3|4|@$0|5|2|6|4|@$0|7|2|8|4|@$0|9|2|A]]]]]|$0|5|2|B]]]" 

# unpack the packed to a clone of the original JSON 	
json = jpy.unpack(packed);
 
print(json);
 
```

## LICENCE

The MIT License (MIT)
Copyright (c) 2013 Rodrigo González, Sapienlab

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.