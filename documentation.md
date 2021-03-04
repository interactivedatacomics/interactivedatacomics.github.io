# Documentation 

This page details the differnet constructs and operations in our specification. For a [tutorial, chere elsewhere](getstarted.html)

This documentation covers: 

* [Panels and Layouts](#panels-and-layout)
* [Data](#data)
* [Operations](#operations)

# Panels and Layout


## Panels
Comics are presented as a series of panenls. Panels can be `.svg` or `.png`. Panels are loaded within their specific array `panels`. Each panel has a positive `id` and which will be used througout the spec to refer to this panel. The 'content' of ech panel is loaded from a `url` pointing to a URL where the image is hosted. You can host your SVGs or PNGs on any server in the world as long as the image or svg is publicly retievable throug a URL.

#### Code example
```json
"panels":[
  {
      "id": 1,
      "url":"mypanels/panel1.svg"
  },
  {
      "id": 2,
      "url":"mypanels/panel2.svg"
   }
]
```

## Comic Layout
The comic layout is specified inside the  `layouts` array. You can specify alternative layouts which a user can load on demand using the **Load layout** operation. One layout needs to be set as the `currentLayout`.

Each layout needs a unique `name`. (*tip:* if you have several panels that are placed together and will be fixed forever (no interaction will dissassemble this panel group), you can export and manege these panels as 'one' panel (one single image).)

```json
"currentLayout": "myLayout",
"layouts": [
   {
      "name": "myLayout",
      "panels": [[1,2,3], [4,5,6]]
   }
]
```
This exmple will load six panels, three in each row. 

## Types of layouts

A layout is modeled as a nested array, e.g., `[[1,2,[3,[4,5]]], [6,7]]` with the first two levels being mandatory. This layout spec will create the following layout:

<img width="400px" src="figures/layout-1.png">

* The first array contains all panels. It is always there. 
* The second level, e.g., `[1,2,[3,[4,5]]]` (red) and `[6,7]` (blue), groups panels into rows. Each array is a new row.
* the third level, e.g., `[3,[4,5]]` (darker red) in our example, puts two panels, the first above the other within the same row.
* The fifth level, e.g., `[4,5]` (darkest red) will place the two panels again side-by-side. 

**Note:** The with of panels depends on the SVG or PNG files. All the engine does is appending these panels and placing them in the layout. When you create your design, you should design a layout and panel sizes that work! 


# Data

Our spec has some contructs to refer to data, helas, we're talking about data comics.

## Classes
Classes group visual elements within your elements into groups. Classes can be used to, e.g., highlight elements or otherwise refer to groups of elements. 

Classes are only possible in `svg` panels and requires the elements you are refering to to have unique IDs, `id="myBar"` in the `svg` file. IDs can be the same across panels, e.g., if you have several panels with a bar chart, the first bar can always be called, e.g., `bar1`.

The following example groups three elements `france`, `germany`, `uk` under the class `countries`. Note that these classes work like classes in CSS, but any class attributes in your `svg` are ignored. 

```json
"classes":{
  "name": "countries",
  "elements":["france", "germany", "uk"]
}
```

## Variables 
Variables store numerical values. Variable values can be shown inside text through a place holder that has the same id to the variable, or used to render a number of ISOTYPE like symbols. Variables can be obatained from data, or through user input, e.g., using a slider (see below). 

The optional `value` field specifies the default value if the variable is not set. 
You can create calculated variables by functions, expressed though `what`. 

The following example specifies variables with a default value. Two variables are based on functions. 

```json
"variables":[
  {
   "name": "movementSpeed",
   "value": 0
  },
  {
   "name": "movementVelocity",
   "value": 0
  },
  {
   "name": "totalMovement",
   "value": 0,
   "what": [
    "(",
    "movementSpeed",
    "+",
    "movementVelocity",
    ")"
   ]
  },
  {
   "name": "totalkm",
   "value": 0,
   "what": [
    "movementSpeed",
    "*2000",
    "+",
    "movementVelocity",
    "*8000"
   ]
  }
]
```


# Operations

Operations are the core of interactive data comics. Operations specify what should happen how.

## Highlight

Highlighting the content (e.g., panels or element) when ``"click"`` or ``"mouseover"`` on a pointed ``"element"`` and changes style of element(s) or class(es) with given ID. Highlighting founctions by changing attribution of an element, its ``"scale"``, ``"bolder"`` and ``"background color"``. This could be used as a visual reference when the authors want audience to look back/forward at a certain panel. For providing clear affordances, it can also be used as a visual feedback or feedforward for interactive elements, e.g., indicating clickable elements or change an element's visual status after being clicked. 

#### Code example
```json
{
   "trigger": "mouseover",   
   "element": "panel_6",
   "operation": "highlight",
   "scale": 1.3,
   "background-color": "#666",
   "url": ""
}
```
## Append
Appends set of panels or layout after given panel, this operation can be used for different narrative purpose, e.g., adding a branch to the storyline from a certain point; provising more details by drilling down from this panel; revealing the answer for a question rised in the panel; hinding a punchline and etc. Note this operation will not romove or replace any panles. If you want remove any panle and load new panels, use "Load layout".
```json
{
   "trigger": "click",
   "element": "panel_6",
   "operation": "append",
   "after": "panel_7",
   "newpanels": ["panel_11"]
}
```

### Load layout
This operation can load a new layout and remove anything else ``"after"`` a specific panel by clicking the ``"element"``. It works similar to an navigating founction in a website. For example, the creator can lead the audience to different versions (e.g., length style or content) of the story by using a global navigation manue on the top of the comic.

```json
{ 
   "trigger": "click",
   "operation": "loadLayout",
   "element": "button2",
   "layout": "mediumLayout",
   "group": "group1",
   "after": "group-name"
 }
```
 
 ### Condition
 Setting a condition for operations, when the opration is triggered, different oprations will run under the condition setted.

```json
{ 
    "trigger": "click",    
    "condition": ["if", "totalC02", "> 10"],
    "operation": "loadlayout"
}
```
```json
{   
    "condition": ["if", "totalC02", "> 10"],
    "operation": "append"
}
```


### Replace
Replace a panel with ``"newpanels"`` after doing ``"click"`` or ``"mouseover"`` on the ``"element". In the example below, ``"panel_12"`` indicates the panel with the ``"id"`` of '12'.
```json
{
   "trigger": "click",
   "element": "panel_4",
   "operation": "replace",
   "replace": "panel_4",
   "newpanels": [
    "panel_12",
    "panel_15"
   ]
  }
```

## UI

### Slider
Turns placeholder named by the same ``"id"`` into a slider. Specify ``"variable"`` (see above in **basics** section), min, max. The length of the slider will be as same as the placehover element.
```json
{ 
   "id": "slider_movementSpeed", 
   "variable":"movementSpeed",
   "min": 0,   
   "max": 100  
}
```

### Isotype
Data in comics can be visualizaed by appending isotype symbles to match ``"variable"`` value, The isotype images are loaded from url in ``"icon"``. The size of each icon can be adjusted in ``"widthIcon"``.
```json
{
   "operation": "isotype",
   "variable": "treeIcon",
   "to": "TreesPlaceHolder",
   "attr": {
    "widthIcon": 4.5
   },
   "icon": "images/CO2Footprint/treeIcon.svg"
  }
```
### Input
xxx
```json
code
```
### lens
link two panels where one panel is ovreview and one panel detail

```json
{
   "operation": 'lens', 
   "trigger": "mouseover",
   'element': "panel_14",
   'linked*': ['panel_15'], 
   'viewport-size': 20%
}
```
### multilayer
allows which layers to be visible

```json
{
   "operation": 'multilayer', 
   "trigger": "click",
   'element': "panel_14",
   'elements':[{
       'id': 1, 'linked':[2,3]}]
}
```
### zoom 
single panel that is zoomable
```json
{
   "operation": "zoom", 
   "trigger": "zoom",
   "element": "panel_14",
   "linked": ["panel_15"]
}
```

