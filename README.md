A compression algorithm for JSON, converted to Python

## Notes

This is a copy of https://github.com/rgcl/jsonpack converted to python   
I have used this regularly in python 3.11, and haven't noticed any issues   

This is cross compatible with the original version of this project, so it is very useful for sending data between javascript and python


## Introduction

jsonpack is a JavaScript program to pack and unpack JSON data.

It can compress to 55% of original size if the data has a recursive structure, example 
[Earthquake GeoJSON](http://earthquake.usgs.gov/earthquakes/feed/geojson/2.5/month) or 
[Twitter API](http://search.twitter.com/search.json?q=Twitter%20API&result_type=mixed). 

Install via:
> $ pip install jsonpackpy

### pack(json)
Retrieve a packed representation of the object

** Parameters **

* object: A valid object

** Returns:** 

* string: the packed string representation of the data


#### Example

```python
import jsonpackpy as jpy

data = {
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
 	
 packed = jpy.pack(data)
 
 print(packed)
 # print:
 # "type|world|name|earth|children|continent|America|country|Chile|commune|Antofagasta|Europe^^^$0|1|2|3|4|@$0|5|2|6|4|@$0|7|2|8|4|@$0|9|2|A]]]]]|$0|5|2|B]]]"

```

### unpack(packed)

Unpack the data in the *packed* parameter

** Parameters **

* packed {string} : The result of call jsonpack.packed(...)

** Return: ** 

* object: the clone of the original object

#### Example

```python
import jsonpackpy as jpy

packed = "type|world|name|earth|children|continent|America|country|Chile|commune|Antofagasta|Europe^^^$0|1|2|3|4|@$0|5|2|6|4|@$0|7|2|8|4|@$0|9|2|A]]]]]|$0|5|2|B]]]" 

# unpack the packed to a clone of the original object	
data = jpy.unpack(packed);
 
print(data);
 
```