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

### 1.1 Drawing Panels

Panels are created using any drawing tool you like. Generally, we distinguish between the follwing two *formats*:

* **Vector graphics:** which can export to the scalable vector graphic (`.svg`) format. Commonly used tools include Adobe Illustrator, [Figma](https://www.figma.com) (which is free to use), Sketch, etc. 
* **Pixel graphics:** export into common `.png` files. The most prominent example tool is Adobe Photoshop, etc.

You can also draw panels by hand, scan them, and save them as `.png` files. 

Creating panels as '.svg' allows for more interactivity than `.png` files because we can describe elements inside the panels and reuse them for interactivity.

In our case, we have drawn the following three panels in Figma, an open vector graphics tool. We must draw any panels that we want to show at any point in our comic. In our example, we start by showing 3 panels and show one more panel on demand. 

When we draw the panels, we should draw them with a specific layout in mind. For example, we can draw the panels in their final layout in Figma like so: 

<p style="background-color:red;">PICTURE</p>


### 1.2 Name elements in SVG panels

To make elements *inside* our panels interactive, we give those elements IDs which will appear as `id` in the SVG file like so: 

`<circle id="myCircle" cx="50" cy="50" r="40"/>`

IDs should be unique inside each panel. 

To create IDs in Figma, simply change the name of an object in the item list on the left. Alternatively, you can open the exported SVG file using any text editor and add the ID attribute as in the example above. 

In our example, we label the three bars in each chart/panel with the IDa `A`, `B`, and `C`. We should label the same element in our comic **always** with the same ID as this allows to, e.g., highlight all occurances of this element later. 

<p style="background-color:red;">UPDATE</p>

### 1.2 Exporting Panels

We now export each panel into its own file, either '.png' or '.svg'. In Figma, we do this by:
* selecting all elements in a panel, including the panel frame,
* grouping these elements ( right-click > Group Selection),
* Select the small `+` sign besides `Export` in the menu on the right
* Change PNG to SVG
* Click the `Export XXX ` button. 

We repeat this for each panel. In our case, we end up with X panels, which we can name as we like: 
* `panel-1.svg`
* `panel-2.svg`
* `panel-3.svg`
* `panel-4.svg`



### 1.3 Store Panels



# Specify Layout



# Specify Data



# Specify Operations
