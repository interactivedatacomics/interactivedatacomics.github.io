# Get Started

Using a simple example, this page gives a step-by-step overview how you can create an interactive data comic using propriatary drawing tools and our [specification](documentation.html). In this example, we will create a simple comic that starts with 2 panels, highlights elements, and adds more panels on demand. 

Check the [final interactive comic in our editor](https://hugoromat.github.io/interactiveComics/library/dist/getStarted.html). 

You can download the [JSON specification for this example here](getstarted/tutorial.json). Read the [documentation](documentation.html) to learn about the other operations.

The specification is written in [Java Script Object Notation (JSON)](https://en.wikipedia.org/wiki/JSON) and is used to specify layouts and interactions on top of a set of drawn comic panels.   

The steps to create an interactive data comic are as follows: 
* [1 Creating Panels](#creating-panels): drawing panels and layout, naming elements in panels and export individual panels. **This step will take most of your time** and does not involve our specification.
* [2 Specify layout](#specify-layout): specify how panels will be laid out in the interactve version.
* [3 Specify operations](#specify-operations): specify what interactive features you would like the comic to have.


# 1 Creating Panels

Panels are the core element of any (interactive)(data) comic and you will spend a significant amount of time scripting and drawing your comic. 

## 1.1 Drawing Panels

Panels are created using any drawing tool you like and are completely creted by you and your creativity. Panels can contain text, images, drawings, and visualizations.  

Generally, we distinguish between the follwing two *formats*:

* **Vector graphics:** which can export to the scalable vector graphic (`.svg`) format. Commonly used tools include Adobe Illustrator, [Figma](https://www.figma.com) (which is free to use), Sketch, etc. **We strongly recommend that you create your panels as a vector graphic**.
* **Pixel graphics:** export into common `.png` files. The most prominent example tool is Adobe Photoshop, etc. You can also draw panels by hand, scan them, and save them as `.png` files. 


**Note:** Creating panels as '.svg' allows for more interactivity than `.png` files because we can describe elements inside the panels and reuse them for interactivity.

In our case, we have drawn the following 8 panels in Figma, an open vector graphics tool. We must draw any panels that we want to show at any point in our comic. In the final comic, start by showing only the first 2 panels and show one more panel on demand. 

When we draw the panels, we should draw them with a specific layout in mind. For example, we can draw the panels in their final layout in Figma. The below image, we show all 8 panels that a user can eventually see in this example since we created them in the same file.

![](getstarted/panels/allpanels.png)

## 1.2 Name elements in SVG panels

To make elements (parts of visualizations, text, buttons, etc.) *inside* our panels interactive, we give those elements IDs which will appear as `id` in the SVG file. To create IDs in Figma, simply change the name of an object in the item list on the left. Alternatively, you can open the exported SVG file using any text editor and add the ID attribute as in the example above. 

In our example, we label the three bars in each chart/panel with the IDa `a`, `b`, and `c`. We should label the same element in our comic **always** with the same ID as this allows to, e.g., highlight all occurances of this element later. 

After exporting the panel (next step), the `panel.svg` should have the IDs showing in the file: 

```svg
<rect id="a" x="121" y="145" width="46" height="200" fill="#C4C4C4"/>
<rect id="b" x="176" y="215" width="46" height="130" fill="#C4C4C4"/>
<rect id="c" x="231" y="275" width="46" height="70" fill="#C4C4C4"/>
```

We also want out 'compare all' button show some more panels. We give all three instances in our panels the id `compare`. 

## 1.3 Exporting Panels

We can now export each panel into its own file, either '.png' or '.svg'. In Figma, we do this by:
* selecting all elements in a panel, including the panel frame,
* grouping these elements ( right-click > Group Selection or `command+G` on Mac),
* Select the small "`+`" sign besides `Export` in the menu on the right
* Change PNG to SVG
* Click the "`...`" button to the right of the "SVG" field and 
* Make sure the "Include "id" Attribute" option is checked. 
* Click the `Export ...` button. 

We repeat this for **each** panel. In our case, we end up with eight SVG files, which we name like so:
* `price.svg`
* `units.svg`
* `sales-a.svg`
* `sales-b.svg`
* `sales-c.svg`
* `sales-a-small.svg`
* `sales-b-small.svg`
* `sales-c-small.svg`

## 1.4 Store Panels Online

Next, we need to store all panels on a public webspace for our software to find them. If you do not have your own server, greate a public and free [GitHub](https://github.com) repository. Then, upload all your panels, which should look like so: 

![](getstarted/panels/files.png)

To get the public URL for each pabel, click on each file and click the `Raw` button in the menu bar just above the panel image: 

![](getstarted/tut-raw.png)

In the new page that opens, copy the URL from your browser window. That is your panel's URL. In our case, we obtained the following URLs. You can use these URLs in for the rest of the tutorial, you do not have to upload these panels again. 

* [https://raw.githubusercontent.com/interactivedatacomics/interactivedatacomics.github.io/main/getstarted/panels/price.svg](https://raw.githubusercontent.com/interactivedatacomics/interactivedatacomics.github.io/main/getstarted/panels/price.svg)
* [https://raw.githubusercontent.com/interactivedatacomics/interactivedatacomics.github.io/main/getstarted/panels/units.svg](https://raw.githubusercontent.com/interactivedatacomics/interactivedatacomics.github.io/main/getstarted/panels/units.svg)
* [https://raw.githubusercontent.com/interactivedatacomics/interactivedatacomics.github.io/main/getstarted/panels/sales-a.svg](https://raw.githubusercontent.com/interactivedatacomics/interactivedatacomics.github.io/main/getstarted/panels/sales-a.svg)
* and to forth. 


Voila, we can now move the scripting language. 

# 2 Specify Layout

The specification is written in [Java Script Object Notation (JSON)](https://en.wikipedia.org/wiki/JSON). You do not have to be familiar with JSON as our specification is quite simple. From here on, you can simply copy-paste our examples and modify them on your own. 

If you have never heard of JSON before, check this brief [introduction](json-intro.html).

All of the following code of this tutorial should be surrounded by a pair of curly brakets "`{}`".

## 2.1 Specify Panels 

First, we load our panels. This happens by specifying the URL and a panel ID for each panel, inside a `panels` array. Effectively, each panel is an object with two attributes (key-value pairs): `id` and `url`.

```json
"panels":[
  {
      "id": 1,
      "url":"https://raw.githubusercontent.com/interactivedatacomics/interactivedatacomics.github.io/main/getstarted/panels/price.svg"
  },
  {
      "id": 2,
      "url":"https://raw.githubusercontent.com/interactivedatacomics/interactivedatacomics.github.io/main/getstarted/panels/units.svg"
  },
  {
      "id": 3,
      "url":"https://raw.githubusercontent.com/interactivedatacomics/interactivedatacomics.github.io/main/getstarted/panels/sales-a.svg"
  },
  {
      "id": 4,
      "url":"https://raw.githubusercontent.com/interactivedatacomics/interactivedatacomics.github.io/main/getstarted/panels/sales-b.svg"
  },
  {
      "id": 5,
      "url":"https://raw.githubusercontent.com/interactivedatacomics/interactivedatacomics.github.io/main/getstarted/panels/sales-c.svg"
  },
  {
      "id": 6,
      "url":"https://raw.githubusercontent.com/interactivedatacomics/interactivedatacomics.github.io/main/getstarted/panels/sales-a-small.svg"
  },
  {
      "id": 7,
      "url":"https://raw.githubusercontent.com/interactivedatacomics/interactivedatacomics.github.io/main/getstarted/panels/sales-b-small.svg"
  },
  {
      "id": 8,
      "url":"https://raw.githubusercontent.com/interactivedatacomics/interactivedatacomics.github.io/main/getstarted/panels/sales-c-small.svg"
  }
]
```

Our engine will retrieve the pictures from these URLs.

## 2.2 Specify Panels 

Second, we need to specify how panels are laid out. The layout design should have happend in the [design phase](#11-drawing-panels).
The panel width for each panel is specified in side each panel SVG or PNG file so that you do not have to care about this in the specification. All we need to do do is to specify the order and when to start a new row. 

Layouts are specified as *nested* arrays using squared brakets `[]`. For our example, we create a layout with 1 row that contains our first two panels `1` and `2`. To that end, we place both numbers into an array `[1,2]` to indicate that they should appear on the *same* row (our specifcation supports a [wide range of layout options](documentation.html#comic-layout)).

Now, we give the layout a `name` and add it to a `layouts` array (give the layout any name you like, here we call it `myLayout`). We move our pabel specification from above (`[1,2]`) into the array of the `"panels"` attribute. The outer array allows us to add more rows later but here, we start with only one row.

```json
"layout": [
   {
      "name": "init",
      "panels": [[1,2]]
   }
]
```

The `layout` array allows you to add multiple layouts and [switch between the layouts  interactively](documentation.html#load-layout). 

Lastly, we need indicate the layout we want to start with: 

```json
"currentLayout": "init"
```

At this point, we can run [our code](gestarted/tutorial-layoutonly.json), missing only the interactions.


# 3 Specify Operations

Now, we can specify operations to make our comic interactive. Any operation is a JSON object in the `operations` array: 

```json
"operations":[]
```

In the following, we specify two operations.

The first operation highlights (`"operation": "highlight"`) all occurances of element `A` when the user hovers (`"trigger": "mouseover"`) any element with the id `a` (`"element": "a"`). The highlighted elements will become red (`"after": {"style": {"fill": "red"}}"`).

The second operation (`"operation": "append"`) shows a new panel below the other panels (`"after": 2`) when the user clicks (`"trigger": "click"`) on any elemnt with the id `a` (`"element": "a"`). The new panel is shown in a new row  (`"newpanels": [[3]]`). 
 
```json
"operations":[
  {   
     "trigger": "mouseover", 
     "element": "a",
     "operation": "highlight", 
     "after": {"style": {"fill": "red"}}
  },
  {
     "trigger": "click",
     "element": "a",
     "operation": "append",
     "after": 2,
     "newpanels": [3]
  }
]
```

Last, we want a click onto the button *compare* to replace the current large panel with the time series to be replaced by three smaller panels showing all three time series at the same time. 

<p style="background-color:red;">INCLUDE CORRECT OPERATION HERE</p>.

Read the [documentation](documentation.html) to learn about the other operations.
