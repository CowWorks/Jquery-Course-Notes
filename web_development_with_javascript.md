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

### Selecting Nodes
