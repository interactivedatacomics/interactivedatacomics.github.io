# Documentation 
Comics are presented as a series of panenls that placed in certain layout that paves a visual narrative. For print comic creators, stories are often told across fixed, pre-determined page counts. While on the screen, the space a comic occupies is suddenly no longer fixed. The data, visualizations, panels, layout, order and storyline will be more dynamic. This tool allows you to control these elements with simple JSON spesicications, which deos not require an creator to have any pre-experience of programing. This documentation includes the descriptions and code examples for each configeration and opration.

The **basics** has Panels, Layout, Variables and Classes, which set up materials that prepared for interactive [**operations**] (#operations).

## Basics


### Panels
The ``"id"`` should be a positive integer, this number will be used to indicate this panel in the operations.
Make sure the image is ``".svg"`` or ``".phg"``, and the ``"url"`` should be a direct url to the image, you can upload your image folder in your own GitHub and copy the image url.

#### Code example
```json
"panels":[
  {
      "id": 1,
      "url":"mypanels/panel1.svg"}
]
```

### layout
Different layouts or different version of contents can be set in ``"layouts": [ ]``, give each layout a name then it could be called directly in the **Load layout** operation. Here are three examples of how to use the an array to build up different layouts. (*tip:* if you have several panels that are placed together and will be fixed forever (no interaction will dissassemble this panel group), you can export and manege these panels as 'one' panel (one single image).)

```json
"layouts": [
   {
      "name": "mediumLayout",
      "panels": [[10,11,12], [13,14,15]]
   }
]
```

### Variables 
``"variables" `` stores all data of the comic, those data might be presented as a number by replacing a place holder that has the same id to the variable ``"name"``. ``"value"`` is the default value you give, and you can define your formula in ``"what"``. The variables setted here can be visualizad by the "isotype" operation.

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

### Classes
If you want manage elements by groups, design the groups in ``"classes"``, assign each group a name for calling in operation. For example, highlighting all elements in the comic relating France.

```json
"classes": [
{
  "name": "countries",
  "elements":["france", "germany", "uk"]
}]
```


## Operations


### Highlight

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
 ### Append
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
Turns bounding box into slider. Specify variable, min, max, tickmarks,... 
```json
{ 
   "id": "slider_movementSpeed", 
   "variable":"movementSpeed",
   "min": 0,   
   "max": 100  
}
```

### Isotype
Append isotype/ match variable value, load image from URI
```json
{
   "operation": "isotype", 
   "variable":"totalMovement",
   "to": "isotypePlaceHolder",
   "icon": "images/fog.png",
   "attr": {
      "widthIcon": 30, 
      "widthContainer": 200
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
code
```
### multilayer
allows which layers to be visible

```json
code
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

