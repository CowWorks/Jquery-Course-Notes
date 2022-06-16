# Browser Objects

### Browser Object Model:
- The Browser object model is a set of javascript objects which allow you to interact with the browser. It's not standarized.

---

### The `window` Object:
- The window object containes diferent objects, properties, and methods that allow us to consult the state of the browser and other elements. I will proceed by listing a few of the methods and objects it contains

- `window.alert(msg)`: A method that shows message alerts in the browser window.

- `window.prompt(msg)`: A method that asks the user for some input

- `window.confirm(msg)`: Shows a pop-up with a message that asks for confirmation from the user.

- `window.console`: An object used to write to the developer console of the browser. It's very useful when we're developing with JavaScript. To write to the console we use the method `window.console.log(msg)`.

- `window.innerHeight` and `window.innerWidth`: Properties that give us info on the actual size of the window.

- `window.screen`: An object that provides properties and methods to work with the screen of the device in which the browser is running. With `screen.width` and `screen.height` we can access the width and height of the screen respectively.

- `window.location`: Represents the URL bar. It allows us to load a new page within the same tab using `location.assign(URL)`.

- `window.close()`: Is a method that closes the tab where it's ran.

- `window.open(URL, target, window_features)`: This method loads a specific resource into a new or pre-existing tab. The `URL` parameter is a string which indicates the URL or path of the resource to be added (NOTE: if this parameter is left empty it will open a blank page). `target` is a string without whitespaces, specifying the name of the tab we're loading the resource into. `window_features` is a string which contains a comma-separated list of window features in the form *name*=*value*. In the case of boolean values you just add the *name* of the value. Some of these features are options like the window's default size, position, whether or not to open a minimal pop-up window, and much more.

> NOTE: Since `window` represents a global object that contains everything else, there are many occasions in which it's not required to reference it. For example, in stead of writing `window.alert(msg)`, you could just write `alert(msg)`.

---

### The `document` Object:
- The `window.document` object contains the structure with the html elements of the documents that is currently loaded in the browser. This object provides us with a series of methods which allow us to manipulate said structure. This structure is commonly known as the *Document Object model* or **DOM**.

- We can create the content of a web page on the run. This means that we don't need to create an HTML file. The way this is done is by using the `document.write(html_text)`. Here's an example: 

```js
let my_window = window.open();

my_window.document.write("<p>This is the content of my_window</p>");
```

- We can also access different HTML elements loaded on the page. When the browser processes an HTML file and encounters an HTML element that can be rendered using JavaScript, an object is automatically generated which corresponds with the HTML element. This way, you can manipulate the HTML element through said object using JavaScript. The object can be identified by it's name (HTML `name` attribute) or it's identifier (HTML `id` attribute). Example:

```html
<form action="" name="my_form">
        <input name="text_box" type="Text" value="Data">
</form>
```

- This generates an object denominated as `my_form` which contains a property named `text_box`

- Using JavaScript, we can access the form in any of the following ways:

```js
window.document.my_form;
window.document.forms[0];
window.document.forms["my_form"];
```

- And we can acces the text input contained within the form in any of the following ways:

```js
window.document.my_form.text_box;
window.document.my_form[0];
window.document.my_form.elements[0];
window.document.forms[0].elements["text_box"];
window.document.forms[0][0];
window.document.forms["my_form"]["text_box"];
```

---

### Collection of Browser Objects:
- As you may have noticed, some objects contain collections of objects. For example, `document` can have multiple forms which are stored in a collection named `forms` or a form may contain various elements which are stored in a collection known as `elements`, which is another property of the form object.

- You can access the objects of a collection with three different methods. 1) In the order they are found in the HTML file. 2) With their `id` or `name`. 3) Using their position inside of their collection.

- Some collections belonging to the `document` object are:
    - `links[]`: links in the document (`<a>`).
    - `images[]`: images in the documnent (`<img>`).
    - `forms[]`: the forms in the document (`<form>`).

- In JavaScript, these collections are known as arrays, and on top of allowing you to access the individual elements, they have some common methods which help us manipulate them. For example, the property `length` allows you to know the amount of elements in a collection.

- Although the methods of element manipulation we've explored allow us to access some HTML elements, they don't allow us to manipulate all. Usually you manipulate the nodes of the DOM tree which is created by the HTML document.

<br>

# DOM API: Node selection and navigation

### DOM tree:

- The DOM (Document Object Model) tree is a structure which is generated when an HTML file gets loaded into a browser.

- The most common structure for the tree contains a root node commonly referred to with the `<html></html>` tag which in turns contains a head (`<head></head>`) node and a body (`<body></body>`) node.

<br>

> NOTE: The head node contains page metadata (title, meta tags, and any other identifiers), while the body node contains the `HTML` code of the website.

<br>

- The DOM tree can be manipulated with JavaScript using the DOM API which defines the following types of nodes:
    - `document`: The root node which holds all other nodes.
    - `element`: Represents every HTML tag.
    - `attr`: Represents every attribute belonging to an HTML tag.
    - `comment`: Represents every comment within the HTML file.

- Each node aforementioned defines a set of methods that allow us to manipulate them.

- In order to modify the DOM and the web page the following steps are needed:
    1. Select the node(s) we want to modify.
    2. Employ methods to manipulate them and in turn modify the web page.

---

### Selecting Nodes:
- There are a few ways to access specific nodes in a document:
    - Using either the nomber of the tags or the name of some of it's attributes (`id` or `class` to be precise).
    - Making queries that use CSS selectors.
    - Using the relationships between nodes and navigating the DOM tree.

---

### Using tags and attributes:
- `getElementsbyTagName(tag)`: This method returns an array with every node contained within a tag. If there are none, the array will be empty.

- `getElementById(ID)`: Returns a node corresponding with the element using the `ID` inputted. If the element doesn't exist, the function will return null.

- `getElementsByClassName(class)`: This method returns an array with the `class` attribute inputted. It can be used with any node, returning the descending nodes which contain the aforementioned tag. If there are none, the array will be empty.

---

### Querying CSS selectors:
- `querySelector(selector)`: This method returns *the first element* which matches the CSS selector (or group of selectors) pased into the function.

- `querySelectorAll(selector)`: In contrast to the previous function, this function returns *all* elements that match the selector as an array.

---

### Navigating the DOM Tree
- Once a node is selected using the previous methods, the following (node) properties and methods can be used to access the nodes it contains:
    - `childNodes`: Is a property which contains an array with the children of a node.
    - `firstElementChild` and `lastElementChild`: Are properties which give access to the first and last child elements of a node respectively. If `firstChild` or `lastChild` are used, the text contained will be included.
    - `parentNode`: Is a property which gives access to the node containing the current node.
    - `nextElementSibling` and `previousElementSibling`: Are properties for accessing the next and previous nodes in the same level. Returns null if there are none. `nextSibling` and `previousSibling` will also include text.
    - `hasChildNodes()`: A method that returns whether the node has children or not.

<br>

> NOTE: When the method is executed (`hasChildNodes()`), the returned value will be `true` if the node has children, and `false` if it doesn't.

<br>

# DOM API: Modificating the DOM Tree

### Node Modification:
- `innerHTML`: Is a property that allows access and modification of the HTML content inside of a node. A string can be assigned to this value in order to modify the content.

- `style`: Is a property that allows for the modification of a node's style. We can use `style.property` to modify a specific property, although you may need to do `style[property]` in cases in which the property has a character like a "-".

---

### Creation and deletion of Nodes:
- `document.createElement(tag)`: Creates a new element with the specified tag.

- `document.createTextNode(text)`: Creates a node of text.

- `[current_node].cloneNode(true/false)`: Creates a duplicate of the current node. The parameter controls whether or not it clones the children of the node.

- `[current_node].appendChild(new_node)`: Adds a new node as a child of `[current_node]`. The new node is added at the end of the list of children.

- `[current_node].insertBefore(new_node, previous_node)`: Adds a new node as a child of `[current_node]`. The new node is added in front of the node identified as `previous_node`.

- `[current_node].replaceChild(new_node, old_node)`: Replaces the child node identified as `old_node` with the node identified as `new_node`.

- `[current_node].removeChild(node)`: Removes the child node identified as `node`.

---

### Modificating an Element's Atrributes:
- HTML elements can have attributes. This implies that we can access and modify those attributes with JavaScript. Modifying attributes could be useful in the event that we want to change the class of an element and in turn change it's CSS properties.

- Since the DOM tree has different types of nodes, access to attributes is only possible with nodes of the `Element` type.

- We can use the following methods to modify the attributes of an element:
    - `[node].hasAttribute(attribute_name)`: Returns a boolean depending on if it has an attribute that matches the one passed in.
    - `[node].getAttribute(attribute_name)`: Returns the value of the attribute matching the passed value `attribute_name`. Returns an empty string or null if the the attribute isn't present.
    - `[node].setAttribute(attribute_name, attribute_value)`:  Sets the value of an attribute on the specified element. If the attribute already exists, the value is updated; otherwise a new attribute is added with the specified name and value. 

---

### Modifying an Element's Classes:
- Every `element` node has a property `classList` which facilitates the modification of an object's classes.

- `[node].classList.add(new_class)`: Adds a new class to the `[node]` specified.

- `[node].classList.remove(existing_class)`: Removes a class from `[node]`.

- `[node].classList.contains(class)`: Returns a boolean indicating whether `[node]` contains `class`.

<br>

# Events

- When a user interacts with a web page, whether it be clicking on some elements, hovering the mouse over them, or scrolling, it produces an internal event.

- An event is a signal within the browser which indicates that an interaction has occured.

- There are many types of different events. Each one has it's own name and all of them are generated by the user. Some examples are:
    - `click` is produced when you click on a button.
    - `mousedown` is produced when you click on an element with the mouse.
    - `keydown` is produced when a key is pressed.
    - `scroll` is produced when you use the scroll bar.
    - `copy` is produced when `Ctrl + C` is used.
    - `load` is produced when a page is loaded on the browser.
    - `offline` is produced when connection to the internet is lost.

<br>

- Based on the way that events work in the browser, interactivity can be programmed by producing actions in response to events.

- Ideally, when an event happens, we want a "notification". We do so by *subscribing* to an event by using an event handler.

---

### Event and Callback Handlers:
- An event handler or listener lets you know when an event has been produced. 

- When subscribing to an event, it is necessary to indicate which action we want to carry out in response to the event. This is known as a *callback*, and in JavaScript it's just a function.

- There are a few different ways to register an element's event. Here are some examples:
    - Although this isn't the best way of doing it, it is possible to directly indicate the event through an attribute in HTML
        ```html
        <div id="button" onClick="alert("A click has ocurred!")">Click me!</div>
        ```
    
    - It is possible to indicate the event through JavaScript as well. This is done by using a property which has a similar name to the event with the addition of the prefix `on`.
        ```js
        function notify() {
                alert("A click has ocurred!");
        }

        let button = document.getElementById("my_button");
        button.onClick = notify;
        ```
    
    - Using the `addEventListener(event, function)` method, the same thing previously displayed can be achieved. The event parameter is the event you're subscribing to, while the function parameter is the function you want to run when the event is produced.
        ```js
        function notify() {
                alert("A click has ocurred!");
        }

        let button = document.getElementById("my_button");
        button.addEventListener('click', notify);
        ```
    
    - The callback function allows for the use of the variable named `this`. Said variable contains a reference to the element that produced the event, which allows us to manipulate it with ease.
        ```js        
        function enter() {
                this.style["font-weight"] = bold;
        }

        let button = document.getElementById("my_button");
        button.addEventListener('mouseenter', enter);
        ```

<br>

---

### Event Propagation:
- As previously stated, each event is produced by an object. If a callback is passed into the corresponding handler, it will be executed when the object detects the specified event.

- Most of the time objects will be contained within other objects, which can be seen in the DOM tree. This means that the event propagates up the DOM tree. Because of this, the parent node is able to detect the event that has taken place.

- In order to further explore the nature of event propagation, take a look at the following example:
```html
<html>
        <head>
                <title>Event Propagation</title>
        </head>
        <body onClick="alert('The body was clicked')">
                <p onClick="alert('The first paragraph was clicked')">
                        Click wherever you feel like clicking.
                </p>
                
                <p onClick="alert('The second paragraph was clicked')">
                        Here's a paragraph that contains
                        
                        <strong onClick="alert('The strong element was clicked')">
                                some strong text, and
                                
                                <emph onClick="alert('The emphasized text was clicked')">
                                        some emphasized text as well.
                                </emph>
                        </strong>
                </p>
        </body>
<html>
```

<br>

- There are a few things going on in that snippet of code:
    1. The body element contains two paragraph elements.
    2. The second paragraph element contains a strong element which in turn contains an emphasized element.
    3. When we click any element, the click event is propagated to every element which contains said element.

---

### Element Events:
- These are the main events which allow us to interact with the user when they do something on the page:
    - `onclick`: When a click is performed on an element.
    - `ondblclick`: When a double click is performed on an element.
    - `onfocus`: When the focus is on an element. When we're talking about focus, we're referring to the mouse hovering over an element.
    - `onblur`: When the focus stops being on an element (usually to change it to a different element).

---

### Mouse Events:
- Mouse events are produced when the user (You're not going to believe it... And, you guessed it.) uses the mouse within an HTML page. Here are some of them:
    - `onmousedown`: When a mouse button is pressed.
    - `onmouseup`: When a mouse button is released.
    - `onmouseover`: When the mouse pointer goes over an element.
    - `onmouseout`: When the mouse pointer exits an element.

---

### Page Events:
- These events are produced solely by the window object. The main events we can listen for on the page are the following (remember that if you plan on using `addEventListener()` you will have to remove the `on` prefix):
    - `onload`: Notifies us when a page has been loaded. It's heavily recommended to register a *callback* for this event which will be responsible for adding the rest of the callbacks since once this event has ocurred, it is a given that all of the elements have been loaded.
    - `onunload`: Notifies us when the content of the page has been unloaded (generally when the page is left).
    - `onresize`: Notifies us that the window size has changed.

---

<br>

# 