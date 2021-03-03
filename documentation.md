# Documentation 

## Operations

### Highlight

Highlighting the content (e.g., panels or element) when click/over a pointed element and changes style of all elements with given ID. This could be used as a visual reference when you want audience to look back at a certain panel. It can also be used as a interaction feedback or feedforward, indicating clickable elements. Highlighting is worked by changing attribution of an element, its scale, bolder and background color.

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
### Load layout
This operation can load a new layout and remove anything else by cklicking an pointed element. It works like an navigating founction in a website. For example, the creator can lead the audience to different versions (e.g., length style or content) of the story by using a global navigation manue above the comic.
#### Code example
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
 
 ### Filter Layout
 Filter layout will show only panels with given ID, this operation allows the audience to filter the panels of their interests. For exa
 #### Code example
```json
{ 
    "trigger": "click",    
    "condition": ["if", "totalC02", > 10],
    "operation": "filter"
}
```
```json
{   
    "condition": ["if", "totalC02", > 10],
    "operation": "append"
}
```
### Load layout
loads a new layout and remove anything else
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
 ### Append
 appends set of panels /layout after given panel
```json
{
   "trigger": "click",
   "element": "panel_6",
   "operation": "append",
   "after": "panel_7",
   "newpanels": ["panel_11"]
}
```
### Replace
Replace a panel with new panels
```json
{
   "trigger": "click",
   "element": "panel_4",
   "operation": "replace",
   "replace": "panel_4",
   "newpanels": [
    "panel_12",
    "panel_15"
   ],
   "flexwrap": false
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
   "linked": ["panel_15"
}
```
### layout
xxx
```json
"layouts": [
   {
      "name": "mediumLayout",
      "panels": [[10,11,12], [13,14,15]]
   }
]
```
### Variables
xxx
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
      "value": ["(", "movementSpeed", "+", "movementVelocity", ")","*10"]
  }
]
```

### Classes
xxx
```json
"classes": [
{
  "name": "countries",
  "elements":["france", "germany", "uk"]
}]
```
### Panels
xxx
```json
"panels":[
  {
      "name": "panel0",
      "url":"mypanels/panel0.svg"}
]
```

  
