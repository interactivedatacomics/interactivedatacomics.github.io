# Get Started

Using a simple example, this page gives a step-by-step overview how you can create an interactive data comic using propriatary drawing tools and our [specification](documentation.html). 

The specification is written in [Java Script Object Notation (JSON)](https://en.wikipedia.org/wiki/JSON) and is used to specify layouts and interactions on top of a set of drawn comic panels.   

The steps we  are as follows: 
* [1 Creating Panels](#creating-panels)
* [2 Specify layout](#specify-layout)
* [3 Specify data](#specify-data)
* [4 Specify operations](#specify-operations)


# 1 Creating Panels

Panels are the core of your (interactive)(data) comic and you will spend a significant amount of time scripting and drawing your comic

## 1.1 Drawing Panels

Panels are created using any drawing tool you like. Generally, we distinguish between the follwing two *formats*:

* **Vector graphics:** which can export to the scalable vector graphic (`.svg`) format. Commonly used tools include Adobe Illustrator, [Figma](https://www.figma.com) (which is free to use), Sketch, etc. 
* **Pixel graphics:** export into common `.png` files. The most prominent example tool is Adobe Photoshop, etc.

You can also draw panels by hand, scan them, and save them as `.png` files. 

Creating panels as '.svg' allows for more interactivity than `.png` files because we can describe elements inside the panels and reuse them for interactivity.

In our case, we have drawn the following three panels in Figma, an open vector graphics tool. We must draw any panels that we want to show at any point in our comic. In our example, we start by showing 3 panels and show one more panel on demand. 

When we draw the panels, we should draw them with a specific layout in mind. For example, we can draw the panels in their final layout in Figma like so: 

<p style="background-color:red;">PICTURE</p>


## 1.2 Name elements in SVG panels

To make elements *inside* our panels interactive, we give those elements IDs which will appear as `id` in the SVG file like so: 

`<circle id="myCircle" cx="50" cy="50" r="40"/>`

IDs should be unique inside each panel. 

To create IDs in Figma, simply change the name of an object in the item list on the left. Alternatively, you can open the exported SVG file using any text editor and add the ID attribute as in the example above. 

In our example, we label the three bars in each chart/panel with the IDa `A`, `B`, and `C`. We should label the same element in our comic **always** with the same ID as this allows to, e.g., highlight all occurances of this element later. 

<p style="background-color:red;">UPDATE</p>

## 1.2 Exporting Panels

We now export each panel into its own file, either '.png' or '.svg'. In Figma, we do this by:
* selecting all elements in a panel, including the panel frame,
* grouping these elements ( right-click > Group Selection),
* Select the small `+` sign besides `Export` in the menu on the right
* Change PNG to SVG
* Click the `Export XXX ` button. 

We repeat this for each panel. In our case, we end up with X panels, which we can give any name we like, e.g.,:
* `panel-1.svg`
* `panel-2.svg`
* `panel-3.svg`
* `panel-4.svg`


## 1.3 Store Panels

Next, we need to store the panel on a public space in the web. If you do not have your own server, greate a public and free [GitHub](https://github.com) repository. Then, upload all your panels, which should look like so: 

<p style="background-color:red;">PICURE</p>

To get the public URL for each pabel, click on each file and click the `Raw` button in the menu bar just above the panel image: 

![](getstarted/tut-raw.png)

In the new page that opens, copy the URL from your browser window. That is your panel's URL. In our case, we obtained the following URLs. You can use these URLs in for the rest of the tutorial, you do not have to upload these panels again. 

* `https://raw.githubusercontent.com/interactivedatacomics/interactivedatacomics.github.io/master/getstarted/panel-1.svg`
* `https://raw.githubusercontent.com/interactivedatacomics/interactivedatacomics.github.io/master/getstarted/panel-2.svg`
* `https://raw.githubusercontent.com/interactivedatacomics/interactivedatacomics.github.io/master/getstarted/panel-3.svg`
* `https://raw.githubusercontent.com/interactivedatacomics/interactivedatacomics.github.io/master/getstarted/panel-4.svg`

Voila, we can now move the scripting language. 

# 2 Specify Layout

## 2.1 JSON

The specification is written in [Java Script Object Notation (JSON)](https://en.wikipedia.org/wiki/JSON). You do not have to be familiar with JSON as our specification is quite simple. From here on, you can simply copy-paste our examples and modify them on your own. 

In a nutshell, JSON consiste of key-value pairs in the form of `"key": value`. The *key*-part is always surrounded by `"`. The *value*-part can be one of four types: 

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
  ]
}
```

Note that intendation is not important but greatly improves readability.



## 2.1 Load Panels 

First, we load our panels. This happens by specifying the URL and a panel ID for each panel, inside the `panels` array. 

```json
"panels":[
  {
      "id": 1,
      "url":"https://raw.githubusercontent.com/interactivedatacomics/interactivedatacomics.github.io/master/getstarted/panel-1.svg"
  },
  {
      "id": 2,
      "url":"https://raw.githubusercontent.com/interactivedatacomics/interactivedatacomics.github.io/master/getstarted/panel-2.svg"
   }, 
   {
      "id": 3,
      "url":"https://raw.githubusercontent.com/interactivedatacomics/interactivedatacomics.github.io/master/getstarted/panel-3.svg"
   },
   {
      "id": 4,
      "url":"https://raw.githubusercontent.com/interactivedatacomics/interactivedatacomics.github.io/master/getstarted/panel-4.svg"
   }
]
```


First, we need to specify how panels are laid out. The panel width for each panel is specified in side each panel SVG or PNG file. All we need to do is tell the order and when to start a new row. 

Layouts are specified as nested arrays or pa. The following example produces the layout in the figure below. To learn more about layouts, check our [documentation](documentation.html#comic-layout).

```json
"layouts": [
   {
      "name": "myLayout",
      "panels": [[1,2,3], [4,5,6]]
   }
]




# Specify Data



# Specify Operations
