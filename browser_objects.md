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

- NOTE: Since `window` represents a global object that contains everything else, there are many occasions in which it's not required to reference it. For example, in stead of writing `window.alert(msg)`, you could just write `alert(msg)`.

---

### The `document` object:
- The `window.document` object contains the structure with the html elements of the documents that is currently loaded in the browser. This object provides us with a series of methods which allow us to manipulate said structure. This structure is commonly known as the *Document Object model* or **DOM**.

- We can create the content of a web page on the run. This means that we don't need to create an HTML file. The way this is done is by using the `document.write(html_text)`. Here's an example: 
```js
1        let my_window = window.open();
2
3        my_window.document.write("<p>This is the content of my_window</p>");
```

- We can also access different HTML elements loaded on the page. When the browser processes an HTML file and encounters an HTML element that can be rendered using javascript, an object is automatically generated which corresponds with the HTML element. This way, you can manipulate the HTML element through said object using JavaScript. The object