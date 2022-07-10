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

# DOM API: Modifying the DOM Tree

### Modifying Nodes:
- `innerHTML`: Is a property that allows access and modifying the HTML content inside of a node. A string can be assigned to this value in order to modify the content.

- `style`: Is a property that allows for the modifying a node's style. We can use `style.property` to modify a specific property, although you may need to do `style[property]` in cases in which the property has a character like a "-".

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

### Modifying an Element's Atrributes:
- HTML elements can have attributes. This implies that we can access and modify those attributes with JavaScript. Modifying attributes could be useful in the event that we want to change the class of an element and in turn change it's CSS properties.

- Since the DOM tree has different types of nodes, access to attributes is only possible with nodes of the `Element` type.

- We can use the following methods to modify the attributes of an element:
    - `[node].hasAttribute(attribute_name)`: Returns a boolean depending on if it has an attribute that matches the one passed in.
    - `[node].getAttribute(attribute_name)`: Returns the value of the attribute matching the passed value `attribute_name`. Returns an empty string or null if the the attribute isn't present.
    - `[node].setAttribute(attribute_name, attribute_value)`:  Sets the value of an attribute on the specified element. If the attribute already exists, the value is updated; otherwise a new attribute is added with the specified name and value. 

---

### Modifying an Element's Classes:
- Every `element` node has a property `classList` which facilitates the modifying an object's classes.

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

# Forms

### Form Events:
- Forms contain their own events, such as:
    - `onclick`: This event is triggered when the mouse clicks over an element. It's generally used with the elements `button` and `submit`.
    - `onchange`: This event is triggered when the user changes the value of a text element. It's often used with the elements `<input  type="text">` or `textarea`. It's also triggered when the user selects an option in a dropdown list (`<select>` element).
    - `onfocus` and `onblur`: Triggered when a user hovers their cursor over an element of the form and when they stop respectively.
    - `onsubmit`: Triggered when a form is submitted.
    - `onreset`: Triggered when the form is reset.

- It should also be noted that pressing the submit button triggers multiple events: `onmousedown`, `onclick`, `onmouseup`, and `onsubmit` to name a few. `onsubmit` is usually employed to validate the fields of the form.

---

### Validating Forms:
- When an input of the `submit` type is clicked, a callback binded to the event `onsubmit` is triggered. This is usually employed to send the information from the form somewhere. The problem is that this happens even if the form is wrong. For this reason the function that is subscribed to the event contains an `event` parameter which allows us to cancel it in the case of an error. In order to cancel it we need to call the function `[event].preventDefault()`.

---

<br>

# An introduction to jQuery

- jQuery is a simple library for JavaScript which follows the "write less, do more" philosophy. This library holds the purpose of simplifying the writing of JavaScript code for the browser. It does so by allowing the use of calls for tasks which would take multiple lines of code in vanilla JavaScript. On top of which, it simplifies a lot of the more complex tasks like AJAX (Asynchronous JavaScript And XML) calls or DOM manipulation.

- The jQuery library allows us to do the following things:
    - Manipulating HTML/DOM.
    - Manipulating CSS.
    - Personalization of the HTML events.
    - Effects and animations.
    - AJAX calls.
    - As well as some other operations.

---

### Installation:
- Installation is as simple as downloading the library and adding it as another script in your HTML page. You can download it from [jQuery.com](https://jquery.com/).

- Another option is using one of the versions stored in what is known as the CDN (Content Delivery Networks):
```html
<script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
```

---

### General Syntax:
- jQuery's syntax is quite simple, and in it's own way, very similar to that of CSS. Generally, the mayority of the calls are made up of a *selector* followed by an *action*: `$(selector).action()`.

- With the $ symbol we access the jQuery module.

- The selector allows us to sellect HTML elements. It's a string which represents a CSS selector like the ones used with the functions `querySelector` and `querySelectorAll`.

- The action is ran on **all** elements selected. In other words, unlike what we used to do with JavaScript, it's unnecessary to loop through the elements if we want to perform the same action on all of them.

- We can target a specific element by using the syntax: `$(selector, parent_element).action()`. In this case we only execute the action on the elements that coincide with `selector` and that are children of `parent_element`.

- It is possible to chain the execution of multiple actions over the same selector. The only requirenment is to add the action after the one in front: `$(selector).action1().action2().action3()`.

---

<br>

# Selectors

- Selectors allow us to indicate what elements from the DOM tree we want to apply an action to. These selectors are the same that are used in CSS. The common ones are:
    - Element
    - Class
    - Identifier

---

### Element Selector:
- It is possible to select an element based on it's HTML tag: `$("p")`. The previous line selects all elements with a paragraph tag.

- Likewise, it is also possible to select elements based on their `id`. In this case we use the # symbol followed by the identifier: `$("#test")`.

---

### Selecting by Class:
- When selecting by class, a method similar to selecting by `id` is used, with the minor change of using the `.` symbol instead of `#`. This allows us to select elements with a given class: `$(".test")`.

---

### Empty Selectors:
- Selectors don't always return an element. For example, if we make a mistake when writing the selector, or we modify the DOM and get rid of an element, the selector won't return any element. This means that when we try to run an action on it, an error will be produced.

- The most common way to know if a selector has found an element is by using the `length` attribute of the element. This attribute contains the amount of elements in the DOM that are characterized by the selector. This means that if the attribute is equal to 0, there are no elements of the type. Here's an example of how that can be utilized:
```js
let elements = $("#thisisnotarealid");

if(elements.length === 0) {
        alert("This selector has no elements");
}
```

---

### More Selectors:

- Like mentioned earlier, the selectors used by jQuery are the same used in CSS. This means that there are a lot more selectors which give us the ability to select different objects. Here's a list of those selectors:
    - `$("*")`: Selects all elements.
    - `$("p.intro")`: This allows us to select a tag (`p`), with the class `intro` (this can be done with any tag and class you have).
    - `$("p:first")`: Selects the first paragraph.
    - `$("ul li:first")`: Selects the first `li` element of the first `ul` element.
    - `$("ul li:first-child")`: Selects the first `li` element of each `ul` element.
    - `$("[href]")`: Selects all elements with an `href` attribute.
    - `$("a[target='_blank']")`: Selects all `a` elements with a `target` attribute with the value of `"_blank"`.
    - `$("a[target!='_blank']")`: Selects all `a` elements with a `target` attribute which doesn't have the `_blank` value.
    - `$(":button")`: Selects all `button` elements, and all `input` of the type `"button"`.
    - `$("tr:even")`: Selects all `tr` (table row) elements which are even.
    - `$("tr:odd")`: Selects all `tr` elements which are odd.

---

<br>

# Events in jQuery

### Syntax for using events in jQuery:
- In order to use events, we employ a selector, followed by the event we want target, and within parenthesis, the function or callback that will be executed in response to said event:
```js
$(selector).event(function(){
        // Code that should run when the event is detected by the selector.
});
```

- An alternative way of doing it is by ussing the action `on`:
```js
$(selector).on(event, function(){
        // Code that should run when the event is detected by the selector.
});
```

- In both cases, the name of the event is the same. Sometimes this is the only way to register the event. For example, a form's `reset` event can only be regfistered in this manner because there's no `$(selector).reset`.

---

### Load Events:
- Given that jQuery can handle the same events as vanilla JavaScript, it is also able to handle `window` events. One of them being the `load` event:
```js
$(window).load(function(){
        //
});
```

- That being said, it's not always necessary to wait for all images, scripts, and icons to load. As long as the DOM is loaded, we can start manipulating it with jQuery. In order to start working with the DOM when it's loaded, jQuery has the following method:
```js
$(document).ready(function(){
        // jQuery code
});
```

- Since it's commonly used, jQuery provides us with a shorter syntax:
```js
$(function(){
        // jQuery code
});
```

---

<br>

# Modifying The DOM Tree

### HTML Elements With jQuery:
- It is possible to create an empty HTML element subtituting the selector with the tag of the element we want to create. For example, in order to create a paragraph we can use the following syntax:
```js
let paragraph = $("<p>");
```

<br>

- If we want to create a div element with a specific class we can use the following syntax:
```js
let element_with_class = $("<div class='my_class'>");
```

<br>

- The content of the HTML elements can be accessed and modified using the following jQuery methods: `text()`, `html()`, and `val()`.

---

### Accessing an Element's Content:
- It's possible ot access the content of the elements in a page using the following methods *without parameters*:
    - `text()`: Returns the content of an HTML element in text form.
    - `html()`: Returns the content while maintaining the HTML tags.
    - `val()`: Is only used to return the value of form's field.

---

### Adding Elements To The DOM:
- Just like JavaScript, jQuery has functionality for modifying the DOM:
    - `append()`: Inserts the parameter as the last child of the selected element.
    - `prepend()`: Inserts the parameter as the first child of the selected element.
    - `after()`: Inserts the parameter after the selected element as a sibling.
    - `before()`: Inserts the parameter before the selected element as a sibling.
    - `wrap()`: Inserts the parameter as the parent node of the selected element.

---

### Removing Elements From The DOM:
- In order to remove HTML elements jQuery has the following functions:
    - `remove()`: Removes the selected node and it's children.
    - `empty()`: Removes all of the children of the selected node.

---

### Modifying and Accessing Attributes With jQuery:
- The method `attr()` can be used to obtain or modify the value of an HTML element. Similarly to `text`, `html`, or `val`, the behavior of `attr` depends on the parameters used:
    - If used with one parameter (the name of the attribute), it will access the value of the specified attribute.
    - If used with two parameters (the name of the attribute and the new value), the existing specified value will be exchanged with the one given.

---

### Modifying and Accessing Properties with jQuery:
- Some elements such as those on forms, have properties that we may want to check or change. For example, the `checked` property of a checkbox indicates whether it's selected or not. In order to access or modify these properties, we use the `prop` action. Similarly to the previous, it can be used with one or two parameters:
    - If used with one parameter (the name of the property), it will access the value of the specified property.
    - If used with two parameters (the name of the property and the new value), the value of the property will change to the one specified in the second parameter.

---

### Modifying The Classes of an Element:
- jQuery also contains methods for adding or removing classes. These are: `addClass()` and `removeClass()` which respectively allow us to add and remove classes from an element. The parameter is the name of the class. It is possible to pass an array of names which you want to add or remove. There's also `toggleClass()` which serves to change between assigning and removing one or more classes. 

---

### Modifying The Style of an Element:
- The `css()` allows us to query or modify any style sheet property of an HTML element. Its operation is simple, similar to the `attr` method that was previously explored:
```js
css(property_name); // This is used to consult the property
css(property_name, value); // This is used to edit the value of the property
```

---

<br>

# Navigation, Looping, and Filtering.

### Navigating Through The DOM Tree:
- jQuery provides some actions which allow for the navigation of the DOM. Here are the primary actions:
    - `parent()`: Selects the paremt element of any selected element.
    - `children()`: Selects the children elements of the selected element. It's very simple to know whether an element has children or not using this method: `children.length()` will return the size of the collection of children.
    - `prev()`: Selects the sibling elements previous to the selected one.
    - `next()`: Selects the sibling elements following the selected one.

- All of these methods accept a selector as a parameter, meaning that it can filter for specific elements. For example: `$("li").parent(".selected")` this snippet of code selects all parent elements of the elements of type `li` that have the `selected` class.

---

### Looping:
- If we use jQuery then we can't iterate through the selected elements with a for loop, like we did directly with JavaScript. In stead, we can loop through the elements in a similar manner to `foreach`, using `each` instead, which recieves a function with two parameters as a parameter"
    - The fist (index) is the number of the element inside of the collection of elements selected.
    - The second (current_element) is the element that we're currently processing.

---

### Filters:
- Filters allow us to specify the elements we want to work with out of a broader collection. Although jQuery contains multiple methods for filtering, we're only going to be focusing on a couple of the simpler ones: 
    - `first()`: Only targets the first element of a collection.
    - `last()`: Only targets the last element of a collection.

<br>

- When the `filter` method is used, the selection focuses on elements from the collection that contain a specific trait or identifier.

---

<br>

# Effects

One of jQuery's features is it's ability to create visual effects with ease: transitions, movements, and animations.

---

### Hide, Show, and Toggle:
- The methods `hide()` and `show()` allow for the hiding or showing of the selected elements respectively. This is done by modifying the element's `display` property. Here's a way of using it for the sake of making a page more interactive:
    - It is possible to indicate the speed by using the strings `"slow"` or `"fast"`, or by indicating the time it should take in milliseconds. In this example: `$(p).hide(1000, myFunction)`, a collection of paragraph elements is selected, they are then hidden within a second, and the function named `myFunction` runs after all of that has happened.

- The `toggle()` method allows an element to switch between `hide()` and `show()` or viceversa. It has the same parameters as the previously mentioned functions. One that dictates the time it should take, and another that runs a function after the act.

---

### Fading:
- The `fadeIn()` method makes a hidden element appear. As parameters it can take the speed as either a value in milliseconds or a string, it can also take a function to be ran after the event.

- The `fadeOut()` method has a behavior opposite to fadeIn and it serves to make an element disappear. It takes in the same parameters as fadeIn.

- Similarly to *hide* and *show*, there's a method for toggling between states. The `fadeToggle()` method serves to toggle between *fadeIn* and *fadeOut*. It should be noted that this method has the same parameters.

---

### Sliding:
- The `slideDown()` method serves to show an element with a dropdown style animation. The speed can be indicated with the values `"slow"` or `"fast"` and, like previous methods a function can be specified to be ran after the method.

- Opposite to `slideDown()`, we have the `slideUp()` method which hides an element with a reduction animation. This method takes in the same parameters as the previous one.

- Yet again we have a toggle method. `slideToggle()` allows you to toggle between the two states.

---

### Animations:
- In the past couple of topics, we have explored some of jQuery's built in animations, that being said, it's about time we got to talking about it's functionality for making custom animations using CSS.

- We can create custom animations in jQuery using the `animate()` method:
```js
$(selector).animate({css properties}, speed);
```

<br>

- The first parameter defines the CSS properties to change. It's possible to animate multiple properties at the same time. These properties are dumped inside of an object and are separated by commas. For each property the final value should be set, the animation method will change the value of the properties to the value passed into the first argument. The method doesn't limit you to one type of value, there are actually a couple of ways to indicate the value the property will have:
    - The final value can be absolute, for example: `width: 100px` will change the width to 100 pixels.
    - The final value can also be relative, for example: `width: '+=100px'` will increase the width by 100 pixels.

<br>

- The second parameter indicates the speed. Just like in previous topics, strings like `fast` and `slow` can be used as well as the time in milliseconds.

- The third argument (optional), allows a function that will be called after the method.

> NOTE: In comparison to the preceding methods, these animations don't modify the visibility of the element, this means that if we want to modify it's visibility, we'll have to do so by acting on it's CSS display property once the animation is over. It should also be noted that in order to chain animations, the third argument should be used to define the new steps for the animation.

---

<br>

# AJAX

AJAX (Asynchronous JavaScript and XML) serves to load and display content on a website without having to reload. Most web apps use this technology nowadays: Gmail, Google Maps, Youtube, Instagram, etc. jQuery makes working with AJAX extremely simple. By usaing jQuery's AJAX methods, we can make calls to a remote server and receive TXT, HTML, XML, or JSON (among a few) documents without having to reload.

---

### The `load()` Method:
- The `load()` method allows for the access and processing of documents from a server in order to use them on the website. The syntax is the following: 
```js
$(selector).load(url, data, callback);
```

<br>

- The selector is the element or collection of elements that the data will be put into.

- `URL` is the URL or location of the server where the data will be fetched from.

- `data` is a plain object or string sent to the server with the request.

- `callback` is a function that's executed when the request completes. It receives 3 parameters:
    - `responseTxt`: A string with the content of the requested document. It will only be valid if the request is processed correctly.
    - `statusTxt`: A string with the state of the request. `success` indicates that the request was successfull. Other strings like: `abort`, `error`, `notmodified`, `parsererror`, or `timeout` represent different errors which can occur when the request is made.
    - `xhr`: Contains an `XMLHttpRequest` with additional information regarding the request and methods for special processing.

---

### Error Handling:
- If the URL in the `load` method is correct, then everything should work fine. In the case that the URL is wrong we will see an error in the debugging console. In order to control errors we can use the callback function and the statusTxt parameter:
```js
function processRequest(responseTxt, statusTxt) {
        
        if(statusTxt != "success") {
                alert("There was an error");
                return;
        }

        this.html(responseTxt);
}

$("button").click(() => {
        $("#ajax").load("data.txt", processRequest);
});
```

---

### Requesting a JSON Document:
- JSON (JavaScript Object Notation) is an open standard file format which is commonly used in the web. This format represents what we recognize as a literal object in javascript, a structure with properties that allows us to group data. For example, we can represent a flight in the following way:
```json
{
        airline: "Oceanic",
        number: 815,
        departure: {
                IATA: "SYD",
                time: "2004-09-22 14:55",
                city: "Sydney"
        },
        arrival: {
                IATA: "LAX",
                time: "2004-09-23 10:42",
                city: "Los Angeles"
        }
}
```

- This format has two main advantages:
    - It's a structured format, which means that it's easier to access the information we need from the document.
    - It's simple to convert it to a javascript object. Other structured formats (like XML) require additional tooling in order to extract the information from the document.

<br>

- In order to convert a string into a literal object we can use the `JSON.parse` method. The return of the method is an object with properties that can be accessed. A simpler way of doing so is with the `$.getJSON` method from jQuery. This method returns an object which can have actions chained to it:
    - The `done(callbackSuccess)` action indicates what we want to do if the request was successful. The callback function receives the object as a parameter.
    - The `fail(callbackError)` action indicates what we want to do if the request fails. The callback function may receive different parameters.

<br>

Here's an example on how a sort of e-mail system could work using the knowledge from this topic:
```json
{
        "Quantity": 3,
        "Mail": [
                {
                       "subject": "The subject of the first mail",
                       "content": "The content of the first mail" 
                },
                {
                        "subject": "The subject of the second mail",
                        "content": "The content of the second mail"
                },
                {
                        "subject": "The subject of the third mail",
                        "content": "The content of the third mail"
                }
        ]
}
```

```js
$(document).ready(function() {
        $("button").click(loadJSON);
});

function loadJSON() {
        $.getJSON("mail.json")
                .done(processRequest)
                .fail(() => {
                        alert("There was an error when loading the file");
                })
}

function processRequest(json) {
        $("#mails").empty().append("<h2>New Mails: " + json.Quantity + "</h2>");

        for(let i = 0; i < json.Mail.length; i++) {
                let mail = json.Mail[i];
                let newMailElement = $("<div class='mail'></div>");

                newMailElement = $(newMailElement).append("<h3>" + mail.subject + "</h3>");
                newMailElement = $(newMailElement).append("<p>" + mail.content + "</p>");

                $("#mails").append(newMailElement);
        }
}
```

<br>

- As can be observed:
    - The `getJSON` function was used instead of `load`. It should be noted that this function needs no selector.
    - After using the function, we first chain the `done` action which has `processRequest` as a callback. The parameter is the object created from the document (mail.json), which we have named `json`.
        - In `processRequest` we work with the object in order to extract it's properties and create DOM elements with them.
        - It should also be noted that `Mail` is an object array, which allows us to iterate through it's content using a for loop.
    - After the `done` action, we chain another action, the `fail` action, which will run in the event that the request fails. When triggered, it will send an alert notifying that something went wrong.

---
