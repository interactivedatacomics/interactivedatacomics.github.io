# Documentation 

## Operations

### Highlight

Highlighting the content (e.g., panels or element) when click/over a pointed element and changes style of all elements with given ID |

#### Code example

   [operations]{
      "trigger": "mouseover",
      "element": "panel_6",
      "operation": "highlight",
      "scale*": 1.3
      "background-color*": #666
      "url*": ""
   }

### Load layout
loads a new layout and remove anything else
#### Code example

   [operations]{ 
      trigger: "click",
      operation: loadLayout,
      element: button2,
      layout: mediumLayout
      group: group1
      after: null | group-name
    }
 
 
 ### Filter Layout
 show only panels with given ID
 #### Code example

   [operations]{ 
       trigger: "click"    
       condition: ["if", totalC02, > 10]
       operation: "filter"
   }
   [operations]{   
       condition: ["if", totalC02, > 10]
       operation: "append"
   }

### Load layout
loads a new layout and remove anything else

   [operations]{ 
      trigger: "click",
      operation: loadLayout,
      element: button2,
      layout: mediumLayout
      group: group1
      after: null | group-name
    }

 ### Append
 appends set of panels /layout after given panel
   [operations]{
      "trigger": "click",
      "element": "panel_6",
      "operation": "append",
      "after": "panel_7",
      "newpanels": ["panel_11"]
   }

### Replace
Replace a panel with new panels

   [operations]{
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
 
## UI

### Slider
Turns bounding box into slider. Specify variable, min, max, tickmarks,... 

   [panel]{ 
      id: slider_movementSpeed', //id of the svg
      variable:'movementSpeed',
      *min: 0,
      *max: 100
   }


### Isotype
Append isotype/ match variable value, load image from URI

   {
      operation: 'isotype', 
      variable:'totalMovement',
      to: 'isotypePlaceHolder',
      icon: 'images/fog.png',
      attr: {'widthIcon': 30, 'widthContainer': 200}
   }

### Input
xxx

   code

### lens
link two panels where one panel is ovreview and one panel detail


   code

### multilayer
allows which layers to be visible


   code

### zoom 
single panel that is zoomable

   {
      "operation": 'zoom', 
      "trigger": "zoom",
      'element': "panel_14",
      'linked*': ['panel_15']
   }

### layout
xxx

   layouts: [
   {name: mediumLayout,
    panels: [[10,11,12], [13,14,15]]
   }]

### Variables
xxx

   variables:[
     {name: 'movementSpeed', *value: 0 },
     {name: 'movementVelocity', *value: 0 },
     {name: 'totalMovement', *value: ['(', 'movementSpeed', '+', 'movementVelocity', ')','*10']}
   ]

### Classes
xxx

   classes: [
   {
     name: 'countries',
     elements:['france', 'germany', 'uk']
   }]
### Panels
xxx
   panels:[
     {name: panel0,url:panels/panel0.svg}
   ]

  
