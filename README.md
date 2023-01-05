# myCherryParser

A program that parses a JSON and creates a CherryTree. Useful to create a initial version of the notes recopiled during an assessment.

myCherryParser creates a XML ".ctd" file from a JSON.


## JSON definition

Cherrytree is formed by a tree of **nodes**. So the JSON will be something similar.

### Node Object

The Node object made up by *info_node*, an array of *content* (`content_node`) and finally an array of *nodes* (`sub_nodes`).

```JSON
{
	"info_node" : {},
	"content_node" : [],
	"sub_node" : []
}
```

### Info_Node Object

The `info_node` object contains information about the node, such as icon, style, color and name.


* `node_name <str>`:  Contains the name that will be displayed on the node.
* `icon <str>`: Contains the icon to display, currently only the following icons are implemented. 

```
redcherry
green
yellow
red
gray
warning
info
question
home
```
* `color <str>`: Describes the color of the text.

```python
black
red
gray
```
* `bold <boolean>`: Boolean type which describes whether the node name is bold.

```JSON
{
	"node_name" : "Hosts",
	"icon" : "warning",
	"bold" : true,
	"color" : "red"
}
```

### Content_Node Array

`content_node` is an array of `contents`. We can add a **text** or an **image**.

#### Image Content

An image content have only two attributes.

* `type <str>`: Which will be `image`.
* `path <str>`: Absolute path of the image to display.

```JSON
{
	"type" : "image",
	"path" : "/tmp/img.png"
}
```

#### Text Content

A Text content have the following attributes.

* `type <str>` : Which will be `text`.
* `string <str>`: Contains the text to display.
* `style <Array <str>>`: Style of the text. Array of styles

```
bold
italic
underline
h1
h2
h3
```

### Sub_Node Array

Each node have an array of subnodes.

## Example of a JSON

```JSON
{
	"info_node" : {
		"node_name" : "Hosts",
		"icon" : "warning",
		"bold" : true,
		"color" : "red"
	},
	"content_node" : [
		{
			"type" : "image",
			"path" : "/tmp/img.png"
		},
		{
			"type" : "text",
			"string" : "Loren Ipsum",
			"style" : [
				"h1",
				"bold",
				"italic"
			]
		}

	],
	"sub_node" : [
		{
			"info_node" : {
				"node_name" : "10.10.10.10",
				"icon" : "home",
				"bold" : true,
				"color" : "red"
			},
			"content_node" : [
				{
					"type" : "text",
					"string" : "NMAP_RESULT",
					"style" : [
						"h1",
						"bold",
						"italic",
						"underline"
					]
				}
			],
			"sub_node" : [
				{
					"info_node" : {
						"node_name" : "Info",
						"icon" : "info",
						"bold" : false,
						"color" : "black"
					},
					"content_node" : [

					],

					"sub_node" : [
						
					]
				}
			]
		},
		{
			"info_node" : {
				"node_name" : "10.10.10.11",
				"icon" : "home",
				"bold" : true,
				"color" : "red"
			},
			"content_node" : [
				{
					"type" : "text",
					"string" : "NMAP_RESULT",
					"style" : [
						"h1",
						"bold",
						"italic"
					]
				}
			],
			"sub_node" : [
				{
					"info_node" : {
						"node_name" : "Info",
						"icon" : "info",
						"bold" : false,
						"color" : "black"
					},
					"content_node" : [

					],

					"sub_node" : [
						
					]
				}
			]
		}
	]
}
```

# Usage

We can parse a JSON with the following command:

```bash
python3 myCherryParser.py input.json output.ctd
```

Or we can import the library to our scripts:

```python
from myCherryParser import *

parser = myCherryParser("input.json", "output.ctd")
parser.parse()
```
