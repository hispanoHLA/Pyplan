# Model
## Node Properties Tabs345
Pyplan structures code trough an influence digram of nodes. When a node is selected (on edit mode) it is open a properties window. Nodes attributes can be inspected and edited trough tabs that are labeled as <kbd>Properties</kbd><kbd>Code</></kbd><kbd>Docs</kbd>.

![enter image description here](http://img.pyplan.org/model-node-prop1.png)
The <kbd>Properties</kbd> tab contains:

 - **Title**: is the legend that will be displayed over the node
 - **ID**: the node identification. The way to call the node values when coding.
 - **Units**: A text value that will be displayed next to the title when evaluating a node.
 - **#**: the number format of the node.
 - **Inputs/Outputs**: list of nodes titles directly linked to the selected node. You can navigate to anyone through clicking on the node name.
 - **Code**: shortcut to the Code tab

The <kbd>Code</></kbd> tab:
![enter image description here](http://img.pyplan.org/model-code-tab1.png)
The code tab presents two windows. The left one is the space to insert the code of the node.
Nodes code **must end with the result definition**. The **"result"** variable contains the output of the node. That is the values to be displayed when the node is evaluated or when called from other node.
Intermediate local variables can be used within the node code. These local variables can be printed in the console for tracing calculation, but at the end must come the result definition.
The right window displays the console output. Any `print()` statement will display outputs here.
When the code is modified, it shows a check and cancel box, and the Play button is turned orange to indicate the node needs to be run. 
 ![](http://img.pyplan.org/model-orange.png)

You can accept changes and run the node by pressing <kbd>Ctrl + Enter</></kbd> or clicking on the icons. 
After running the node the Play button is turned blue to indicate it has already been calculated.
![enter image description here](http://img.pyplan.org/model-blue.png)

The <kbd>Docs</kbd> tab:
This tab a complete HTML text editor to include rich text, links, images and videos that describes and explain the fundamentals of every calculation step. In this way, the app becomes an interactive knowledge repository.
![enter image description here](http://img.pyplan.org/model-docs.png)
## Type of Nodes
The main elements for creating the app calculation logic are the following:

<img src="http://img.pyplan.org/model-nodes-type.png"
	style="float: right; margin-left: 10px;"
	ALIGN=”top”
	height="300" /> 

### Node
Is the main element for creating the calculation logic. It is like a global variable for programming and its definition ends defining the output value of the variable as:

    localvar = 5
    result = 'this is the ouput:' + str(localvar*2)

### Function
This element is used for creating user defined functions.
It follows below a basic example of a UDF definition:

    def _fn(param1,param2):
	    return param1+param2
    result = _fn
Functions can be globally used in the entire model, and custom libraries can be created grouping functions inside a module for later export and import. 

### Decision
A decision node is meant to create a choice for the model user to decide about an option.
Its definition syntax is:

    result = selector(['A','B','C'],1,False)
 where the first parameter is the list of values to be choosing from, the second is the position of the list chosen and the third es a flag to indicate multiple selection option.
 
### Index
[Xarray data structure](http://xarray.pydata.org/en/stable/data-structures.html) is xarray’s implementation of a labeled, multi-dimensional array. It has several key properties:

-   `values`: a  [`numpy.ndarray`](https://docs.scipy.org/doc/numpy/reference/generated/numpy.ndarray.html#numpy.ndarray "(in NumPy v1.16)")  holding the array’s values 
-   `dims`: dimension names for each axis (e.g.,  `('x',  'y',  'z')`)
-   `coords`: a dict-like container of arrays (_coordinates_) that label each point (e.g., 1-dimensional arrays of numbers, datetime objects or strings)

The Pyplan index node is defined as a Pandas index to help operate with Xarray matrix. 
Defining the index it is set the dims and coords properties simultaneously. Dim is defined as the Id property of index and Coords as the elements of the index.
Creating and working with index in this way warranties the domain of matrix operations. So for example when you add two matrix that share an index, they are values defined for all elements of the index. Working with Xarray native dims and coords do not guarantee that, because could be the case that you operate with matrix that even sharing a dimension, coords domain do not intersect.
Index defined in Pyplan have an additional function when creating User Interfaces. When there are more than one Xarray output node that share a dimension, inserting that dimension in the interface will work as a coordinated filter on all objects that share that dimension.

### Button
A button is created as a way to run scripts that make use of the model.
Any custom task, like for example assigning a value or definition to a node, can be executed running a button. Different than nodes its definition do not require the `result = ` sentence at the end, since there is no result to be stored. 

### Module
Modules are the containers of diagrams (workflows of nodes). You can enter into a module double clicking on it. The module navigation path is shown at the top of the digram. You can navigate directly by clicking to the corresponding level you want to go to.
You can drag a group of selected nodes into a module to organize your diagram. Or cut and paste a group in the case you want to move upstream.

### Text
The text node is intended for clarification of the calculation logic. 
Its properties includes text Size that can be adjusted when selecting. Z position, bringing selection to front or sending it back. Text font type and size, and border and background color.
![enter image description here](http://img.pyplan.org/model-text-usage.png)

## Model Preferences

### Default imports
In order to avoid declaring the 'Import' sentence en each node, there is a node, called Default imports that collects the Libraries that will not require to declare import all across the model.

    import numpy, pandas, cubepy, xarray
    #fill the following dict keys with the alias you need to import in each node
    result = {
    "np":numpy,
    "pd":pandas,
    "cubepy":cubepy,
    "xr":xarray}

## Using Python libraries
Pyplan includes a function called install_library to help working with libraries than are not natively included with Pyplan app.
The function is called install_library and its syntax is as shown below

    install_library( pypi_name, import_name=None )
    # for example
    install_library( 'bokeh', import_name=None )
When a node with that instruction is run for the first time, the mentioned library will be installed in a folder included in the folder where the model is saved. A new folder named `libs` will be created and all library components will be installed on that folder.
The image below below show the result of installing the [Bokeh](https://bokeh.pydata.org/en/latest/) visualization library

    install_library( 'bokeh', import_name=None )

![enter image description here](http://img.pyplan.org/model-install-lib.png)

## Toolboxes

<img src="http://img.pyplan.org/model-toolboxes.png"
	style="float: right; margin-left: 10px;"
	ALIGN=”top”
	height="300" /> 
Toolboxes are specific purpose nodes, whith custom wizards associated to them in order to help parametrize a function for producing certain result.
Pyplan includes a toolbox named Data Sources. An example of this wizard has been developed with the read CSV node.
This is an experimental feature. Further development of toolboxes will be mainly driven by Pyplan users requests.
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE0OTE4MDU4OTUsLTY4NTI1ODQ4Niw5NT
QwMTY5MTMsLTI2NjIwNDc1NSwyMDcyMzk5NzY1LDcxMTk3OTUy
MiwtMTAzMTc4ODMzNywyNDY4NDY3MTksLTYxNzQ0NjAxMCwtMT
YzNTYxODgwMSwtMTc2MjYyMjM1Niw4ODY1OTM3MTIsLTM3NjU0
MDEyMywtOTUzNzM3Mzg2LC0xMjYyOTM5MzcxLC03ODA5ODk3Mj
QsLTE4NTg4NDI0NjAsODYyMjQyMTUsLTM5NDMxOTc2NSwxMzE3
MDc3OTUyXX0=
-->
