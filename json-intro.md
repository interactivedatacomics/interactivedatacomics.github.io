# JSON in a Nutshell

JSON consists of key-value pairs in the form of `"key": value`. The *key*-part is always surrounded by `"`. The *value*-part can be one of four types: 

### Numbes 
Numbers are written as `123`, `1`, `1.0`, `0.545`, `.545`.

### Text

Text (*strings*) are written inside `"`: `"some text here"`.

### Arrays 

An array is a list of objects, written inside `[` and `]`, separated by commas: `[1,2,3]`, `["hello","my","friend!"]`.

### Objects

An object (hence the name *object notation*) is another set of key-value pairs, written inside  `{` and `}`, separated by commas: 
 
```json
{
  "name": "Bert", 
  "age": 28, 
  "hobbies":[
    "reading", 
    "drawing", 
    "walking"
  ], 
  "lives in": {
     "name": "Edinburgh", 
     "country": "UK"
  }
}
```
As you see, objects can contain objects, which in turn can contain other objects and so on. Note that intendation is not important but greatly improves readability.
