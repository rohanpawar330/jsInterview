# jsInterview

- [HTML & HTML5 diff](#HTML-&-HTML5-diff)
- [browser view document view](#browser-view--document-view)
- [Center Elements in HTML with Different Methods](#center-elements-in-html-with-diff)
- [Check Browser in User's Machine](#check-browser-in-user-machine)
- [Context ('this') in JavaScript](#context--this-in-js)
- [Currying in JavaScript](#curring-in-js)
- [Data Types in JavaScript](#data-types-in-js)
- [Deep Copy of an Object via Recursion](#deep-copy-via-recursion)
- [Difference Between map() and forEach() in JavaScript](#diff-btw-map-foreach-in-js)
- [Different Ways to Create Objects in JavaScript](#different-ways-to-create-objects-in-js)
- [Document Object Model (DOM)](#dom)
- [Even-Odd Coloring in CSS](#even-odd-coloring-in-css)
- [Event Capturing and Event Bubbling in JavaScript](#event-capturing-and-events-bubbling-in-js)
- [First-Class Functions and Pure Functions in JavaScript](#first-class-function-and-pure-function-in-js)
- [HTML vs HTML5 Differences](#html--html5-diff)
- [Input Types in HTML5](#input-types-in-html5)
- [Is There Another Option Besides Explicit Promises to Handle Asynchronous Code in JavaScript?](#is-there-another-option-besides-explicit-promises-to-handle-asynchronous-code-in-javascript)
- [Macro, Micro, and Event Loop](#macro-micro--event-loop)
- [Positioning in CSS and Its Types](#positioning-in-css-types)
- [Prototype and Prototype Inheritance in JavaScript](#prototype-and-prototype-inheritance-in-js)
- [Pseudo-classes and Pseudo-elements](#pseudo-classes--pseudo-element)
- [Selectors in CSS](#selectors-in-css)
- [Synchronous, Asynchronous, and AMD Functions in JavaScript](#synchronous-amd-asynchronous-functions-in-js)
- [Types of Storage in JavaScript](#type-of-storage-in-js)
- [var, let, and const in JavaScript](#var-let--const-in-js)
- [Webpack and Parcel Comparison](#webpack-and-parcel-comparison)
- [Differences Between Arrow Functions and Function Expressions](#what-are-the-differences-between-arrow-functions-and-function-expressions)
- [Five Key Data Structures in JavaScript](#what-are-the-five-key-data-structures-in-js)
- [Closure in Programming](#what-does-closure-mean-in-programming)
- [Generics in TypeScript](#what-is-generics-in-typescript)
- [Difference Between a Type and an Interface in TypeScript](#what-is-the-difference-between-a-type-and-an-interface-in-typescript)
- [Why is Fetch the Preferred Way to Send a Network Request via the Web Browser in JavaScript?](#why-is-fetch-the-preferred-way-to-send-a-network-request-via-the-web-browser-in-js)

[[^]](#jsinterview)

## HTML & HTML5 diff

Here are the key differences between HTML and HTML5, presented in a point-wise and raw form:

1. Doctype declaration:

   - HTML: `<!DOCTYPE html>`
   - HTML5: Remains the same

2. Structure:

   - HTML5 introduces new structural elements or semantic tags ( which has a meaning full tags apart from creating own header and other ):

   "These semantic tags helps in "

   - SEO
   - Ease to read & Scan HTML
   - better for screen reader and accessibility
     - `<header>`
     - `<nav>`
     - `<section>`
     - `<article>`
     - `<aside>`
     - `<footer>`

3. Form input types:

   - HTML5 introduces new input types:
     - `date`
     - `time`
     - `email`
     - `number`
     - `range`
     - `search`
     - `url`
     - `color`

4. Multimedia support:

   - HTML5 has native support for multimedia:
     - `<video>` element
     - `<audio>` element

5. Canvas and SVG:

   - HTML5 introduces:
     - `<canvas>` element for dynamic graphics and animations
     - Native support for scalable vector graphics (SVG)

6. Geolocation:

   - HTML5 provides a built-in Geolocation API for obtaining user's location

7. Local storage:

   - HTML5 introduces the `localStorage` object for client-side data storage

8. Semantic markup:
   - HTML5 encourages the use of semantic markup for improved accessibility and SEO
   
[[^]](#jsinterview)

## DOM

The DOM is created when a web page is loaded into a web browser. The browser parses the HTML document and constructs a representation of the document in memory as a DOM tree.

This tree structure allows developers to access and manipulate the elements and content of the web page dynamically using programming languages like JavaScript.

[[^]](#jsinterview)

## Browser View & Document View

- Browser View:

  - Also known as "Normal" or "Page" view.
  - Default mode in web browsers for displaying web pages.
  - Renders HTML, CSS, and JavaScript to create the visual representation of a web page.
  - Includes content, layout, and styling.
  - Enables users to view and interact with website features.
  - Supports clicking links, submitting forms, and interacting with multimedia elements.

- Document View:
  - Also known as "Source" or "HTML" view.
  - Allows viewing the underlying HTML source code of a web page.
  - Displays raw HTML markup instead of the rendered representation.
  - Useful for developers and web designers.
  - Helps examine page structure, analyze code, troubleshoot issues, or make modifications.
  - Provides a technical perspective on the web page's building blocks.

[[^]](#jsinterview)

## Check Browser in user machine

To detect the version of the browser in the JavaScript we need to use `navigator.appVersion` or `navigator.userAgent`.

```js
// Check the user agent string
var userAgent = navigator.userAgent;

// Create regular expressions to match common browsers
var chromeRegex = /Chrome\/(\d+)/;
var firefoxRegex = /Firefox\/(\d+)/;
var safariRegex = /Safari\/(\d+)/;
var edgeRegex = /Edg\/(\d+)/;
var ieRegex = /Trident\/(\d+)/;

// Function to extract the browser name and version
function getBrowserInfo(userAgent) {
  if (chromeRegex.test(userAgent)) {
    return { name: "Chrome", version: RegExp.$1 };
  } else if (firefoxRegex.test(userAgent)) {
    return { name: "Firefox", version: RegExp.$1 };
  } else if (safariRegex.test(userAgent)) {
    return { name: "Safari", version: RegExp.$1 };
  } else if (edgeRegex.test(userAgent)) {
    return { name: "Microsoft Edge", version: RegExp.$1 };
  } else if (ieRegex.test(userAgent)) {
    return { name: "Internet Explorer", version: RegExp.$1 };
  }

  // If the browser is not recognized, return null
  return null;
}

// Get the browser information
var browserInfo = getBrowserInfo(userAgent);

// Output the browser name and version
if (browserInfo) {
  console.log("Browser:", browserInfo.name);
  console.log("Version:", browserInfo.version);
} else {
  console.log("Browser information not available.");
}
```

[[^]](#jsinterview)

## Type of storage in js

In JavaScript, there are several types of storage options available for storing data:

1. Local Storage: The Local Storage API allows you to store key-value pairs in the user's web browser. The data stored in local storage remains persistent even after the browser is closed and reopened. It provides a simple and synchronous API for storing and retrieving data. You can use the `localStorage` object to access and manipulate local storage data.

2. Session Storage: Similar to local storage, the Session Storage API also allows you to store data as key-value pairs in the user's web browser. However, the data stored in session storage is tied to a specific browser tab or window session. Once the tab or window is closed, the data is cleared. It provides a similar API to local storage and can be accessed using the `sessionStorage` object.

3. Cookies: Cookies are small text files that are stored in the user's browser. They are commonly used for storing user preferences, session information, or tracking data. Cookies have limitations in terms of the amount of data they can store (usually limited to a few kilobytes) and are sent to the server with each HTTP request. You can create, read, and delete cookies using the `document.cookie` property.

4. \*IndexedDB: IndexedDB is a powerful client-side database system that allows you to store and retrieve large amounts of structured data. It provides an asynchronous API for working with databases and supports advanced querying and indexing capabilities. IndexedDB is well-suited for web applications that require complex data management and offline capabilities.

[[^]](#jsinterview)

## Webpack and parcel comparison

Webpack and Parcel are both popular bundlers for JavaScript applications, but they have some differences in terms of features, configuration, and performance. Here's a comparison between Webpack and Parcel:

1. Configuration:

   - Webpack is highly configurable but requires more manual configuration. It provides a rich ecosystem of loaders and plugins, allowing you to customize every aspect of your build process.

   - Parcel focuses on zero-configuration setups, aiming to provide an out-of-the-box experience with sensible defaults. It automatically handles most common configurations, requiring minimal setup.

2. Development Server:

   - Webpack includes a built-in development server called webpack-dev-server. It offers features like hot module replacement (HMR) to update modules without refreshing the entire page.

   - Parcel also provides a development server with similar features, making it easy to test and iterate on your application during development.

3. Asset Handling:

   - Webpack requires explicit configuration for handling different types of assets, such as CSS, images, or fonts. You need to set up appropriate loaders to process and bundle these assets.

   - Parcel, on the other hand, has built-in support for various file types out of the box, allowing you to import them directly in your code without additional configuration.

4. Performance:

   - Parcel is known for its fast and zero-configuration builds. It achieves this by utilizing an optimized dependency graph and parallelizing the build process.

   - Webpack, while more flexible and powerful, may require additional optimization techniques and configuration to achieve optimal performance for large-scale projects.

5. Code Splitting:

   - Webpack has extensive support for code splitting, allowing you to split your code into multiple chunks that can be loaded on-demand. This feature is beneficial for optimizing the initial load time and reducing the size of the bundle.

   - Parcel also supports code splitting, but it does so automatically without requiring explicit configuration. It analyzes the module dependencies and creates separate bundles accordingly.

6. Ecosystem and Community:

   - Webpack has a mature and robust ecosystem with a large community and extensive documentation. It has been widely adopted and offers a wide range of plugins and loaders created by the community.

   - Parcel, although newer, has gained popularity for its simplicity and ease of use. While its ecosystem is not as extensive as Webpack's, it still provides support for common features and has an active community.

Overall, if you prefer a **highly customizable and configurable bundler with a mature ecosystem, Webpack may be the better choice**. On the other hand, if you value **simplicity, zero-configuration setups, and fast development iterations, Parcel provides a great out-of-the-box experience**. The choice between Webpack and Parcel ultimately depends on your project's requirements, complexity, and your preference for configuration flexibility versus zero-configuration simplicity.x

[[^]](#jsinterview)

## input types in HTML5:

1. Text: `<input type="text">` - A single-line text input field where users can enter alphanumeric text.

2. Password: `<input type="password">` - Similar to a text input field, but the entered characters are masked to hide the actual content (typically used for passwords).

3. Number: `<input type="number">` - Allows users to enter numeric values. Some browsers provide additional controls like increment and decrement buttons.

4. Email: `<input type="email">` - Validates the entered value to ensure it is in a valid email format.

5. URL: `<input type="url">` - Validates the entered value to ensure it is in a valid URL format.

6. Checkbox: `<input type="checkbox">` - A checkbox that allows users to select multiple options.

7. Radio: `<input type="radio">` - Radio buttons allow users to select only one option from a list of choices.

8. Date: `<input type="date">` - Provides a date picker or calendar to select a specific date.

9. Time: `<input type="time">` - Allows users to enter or select a specific time.

10. File: `<input type="file">` - Allows users to upload files from their device.

11. Color: `<input type="color">` - Provides a color picker to select a specific color.

12. Range: `<input type="range">` - Renders a slider control that allows users to select a value within a specified range.

13. Search: `<input type="search">` - Renders a search input field with built-in search functionality.

14. Submit: `<input type="submit">` - A button that submits the form data to the server.

15. Reset: `<input type="reset">` - A button that resets the form fields to their default values.

[[^]](#jsinterview)

## Positioning in CSS Types

1. **Static**: The default position type for elements. Elements with `position: static` are positioned according to the normal flow of the document. Top, right, bottom, left, and z-index properties have no effect on statically positioned elements.

2. **Relative**: Elements with `position: relative` are positioned relative to their normal position in the document flow. When you apply top, right, bottom, or left properties, the element will be shifted from its original position, but the space it occupied originally will still be reserved.

3. **Absolute**: Elements with `position: absolute` are positioned relative to their nearest positioned ancestor (parent element with a position other than static) or to the initial containing block if there is no positioned ancestor. An absolutely positioned element is taken out of the normal document flow, and other elements will ignore the space it occupied.

4. **Fixed**: Elements with `position: fixed` are positioned relative to the viewport (the browser window) and will stay fixed in that position even if the page is scrolled. It is commonly used for creating elements such as sticky headers or fixed navigation menus.

5. **Sticky**: Elements with `position: sticky` are positioned based on the user's scroll position. It acts as a hybrid between `position: relative` and `position: fixed`. The element is initially positioned according to the normal flow but becomes fixed once the user scrolls to a certain threshold. It then behaves like a fixed element relative to its containing block.

6. **Inherited**: In addition to the above position types, there is also the "inherited" position value. It means that an element inherits the position value from its parent. This is the case when the position property is not explicitly set on the element.

[[^]](#jsinterview)
## Center elements in html with diff

There are several ways to center elements in HTML and CSS. Here are a few commonly used methods:

1. Using CSS Flexbox:

   ```html
   <div class="container">
     <div class="centered-element">Centered Content</div>
   </div>
   ```

   ```css
   .container {
     display: flex;
     justify-content: center;
     align-items: center;
     height: 100vh; /* Adjust as needed */
   }
   ```

2. Using CSS Grid:

   ```html
   <div class="container">
     <div class="centered-element">Centered Content</div>
   </div>
   ```

   ```css
   .container {
     display: grid;
     place-items: center;
     height: 100vh; /* Adjust as needed */
   }
   ```

3. Using CSS Positioning (Absolute and Transform):

   ```html
   <div class="container">
     <div class="centered-element">Centered Content</div>
   </div>
   ```

   ```css
   .container {
     position: relative;
     height: 100vh; /* Adjust as needed */
   }

   .centered-element {
     position: absolute;
     top: 50%;
     left: 50%;
     transform: translate(-50%, -50%);
   }
   ```

4. Using CSS Positioning (Absolute and Margins):

   ```html
   <div class="container">
     <div class="centered-element">Centered Content</div>
   </div>
   ```

   ```css
   .container {
     position: relative;
     height: 100vh; /* Adjust as needed */
   }

   .centered-element {
     position: absolute;
     top: 50%;
     left: 50%;
     transform: translate(-50%, -50%);
     margin: 0 auto;
   }
   ```

5. Using CSS Text Alignment (for inline or inline-block elements):

   ```html
   <div class="container">
     <span class="centered-element">Centered Content</span>
   </div>
   ```

   ```css
   .container {
     text-align: center;
     height: 100vh; /* Adjust as needed */
   }

   .centered-element {
     display: inline-block;
   }
   ```

## Selectors in css

CSS selectors are patterns used to select and target specific HTML elements for styling.

1. Element Selector: Targets elements based on their HTML tag name. For example:

   ```css
   p {
     /* Styles applied to all <p> elements */
   }
   ```

2. Class Selector: Targets elements with a specific class attribute value. Class names are preceded by a dot (.). For example:

   ```css
   .my-class {
     /* Styles applied to elements with class="my-class" */
   }
   ```

3. ID Selector: Targets a specific element based on its unique ID attribute value. ID names are preceded by a hash (#). For example:

   ```css
   #my-id {
     /* Styles applied to the element with id="my-id" */
   }
   ```

4. Attribute Selector: Targets elements based on their attribute values. For example:

   ```css
   input[type="text"] {
     /* Styles applied to <input> elements with type="text" */
   }
   ```

5. Descendant Selector: Targets elements that are descendants of a specific parent element. It uses a space between the selectors. For example:

   ```css
   .parent-class span {
     /* Styles applied to <span> elements that are descendants of elements with class="parent-class" */
   }
   ```

6. Child Selector: Targets direct child elements of a specific parent element. It uses the greater-than sign (>). For example:

   ```css
   .parent-class > span {
     /* Styles applied to <span> elements that are direct children of elements with class="parent-class" */
   }
   ```

7. Adjacent Sibling Selector: Targets elements that come immediately after another element. It uses the plus sign (+). For example:

   ```css
   h2 + p {
     /* Styles applied to <p> elements that come immediately after <h2> elements */
   }
   ```

8. General Sibling Selector: Targets elements that are siblings of another element. It uses the tilde (~). For example:

   ```css
   h2 ~ p {
     /* Styles applied to <p> elements that are siblings of <h2> elements */
   }
   ```

9. Pseudo-Classes and Pseudo-Elements: Pseudo-classes allow you to select elements based on their state or position, such as `:hover`, `:active`, `:nth-child()`, etc. Pseudo-elements target specific parts of an element, such as `::before`, `::after`, `::first-line`, etc.

[[^]](#jsinterview)

## Pseudo Classes & Pseudo Element

A colon **(:) for pseudo-classes** and two colons **(::) for pseudo-elements**.

Pseudo-Classes:

1. :hover - Targets an element when the mouse pointer is over it.
2. :active - Targets an element when it is being activated or clicked.
3. :focus - Targets an element when it has focus (such as when it is selected via keyboard navigation).
4. :visited - Targets links that have been visited.
5. :first-child - Targets the first child element of its parent.
6. :last-child - Targets the last child element of its parent.
7. :nth-child(n) - Targets elements that match a specific position or pattern within their parent.
8. :nth-of-type(n) - Targets elements of a specific type that match a specific position or pattern within their parent.
9. :not(selector) - Targets elements that do not match a specific selector.

Pseudo-Elements:

1. ::before - Inserts content before the content of an element.
2. ::after - Inserts content after the content of an element.
3. ::first-line - Targets the first line of text within an element.
4. ::first-letter - Targets the first letter of text within an element.
5. ::selection - Targets the portion of text selected by the user.

Here are a few examples of how pseudo-classes and pseudo-elements can be used in CSS:

```css
/* Pseudo-classes */
a:hover {
  /* Styles applied to links when hovered over */
}

input:focus {
  /* Styles applied to input elements when they have focus */
}

li:first-child {
  /* Styles applied to the first child of a list */
}

/* Pseudo-elements */
p::first-line {
  /* Styles applied to the first line of text within paragraphs */
}

div::before {
  /* Styles to insert content before the content of div elements */
}

p::after {
  /* Styles to insert content after the content of p elements */
}

::selection {
  /* Styles applied to the selected text */
}
```

[[^]](#jsinterview)

## Even odd coloring in CSS

In CSS, the `:nth-child()` pseudo-class allows you to select elements based on their position within a parent container. One of the common uses of `:nth-child()` is to apply styles to elements based on their odd or even positions. Here's how it works:

The `:nth-child(odd)` pseudo-class selects elements that have odd positions within their parent container, while `:nth-child(even)` selects elements with even positions. The numbering starts from 1.

For example, consider an unordered list (`<ul>`) with list items (`<li>`). You can apply different styles to the odd and even list items using `:nth-child(odd)` and `:nth-child(even)` selectors:

```css
li:nth-child(odd) {
  background-color: #f2f2f2; /* Apply a background color to odd list items */
}

li:nth-child(even) {
  background-color: #ffffff; /* Apply a different background color to even list items */
}
```

[[^]](#jsinterview)

## Prototype and Prototype Inheritance in JS

In JavaScript, the prototype is an internal property of every object that allows objects to inherit properties and methods from other objects. It forms the basis for prototype-based inheritance in JavaScript. Let's explore the concepts of prototype and prototype inheritance:

1. Prototype:

   - Every object in JavaScript has a prototype property, which can be accessed using `Object.getPrototypeOf(object)` or `object.__proto__`.
   - The prototype property is a reference to another object, often called the object's "prototype."
   - The prototype object contains properties and methods that are shared among all instances created from the same constructor function or class.
   - When you access a property or method on an object, JavaScript first looks for it on the object itself. If it doesn't find it, it searches for it in the object's prototype, and continues up the prototype chain until it finds the property or reaches the top-level `Object.prototype`.

2. Prototype Inheritance:
   - Prototype inheritance allows objects to inherit properties and methods from their prototype objects.
   - When you create a new object using a constructor function or the `class` syntax, the prototype of the newly created object is set to the constructor function's `prototype` property or the class's `prototype`.
   - By adding properties and methods to the prototype of a constructor function or class, those properties and methods become accessible to all instances created from that constructor function or class.
   - Inheritance is achieved by setting an object's prototype to another object. This can be done using the `Object.create()` method or by directly assigning the prototype using `object.__proto__` (although direct manipulation of `__proto__` is generally not recommended).

Here's an example to illustrate prototype and prototype inheritance:

```javascript
// Constructor function
function Person(name) {
  this.name = name;
}

// Adding a method to the prototype
Person.prototype.greet = function () {
  console.log("Hello, my name is " + this.name);
};

// Creating instances of Person
const person1 = new Person("Alice");
const person2 = new Person("Bob");

person1.greet(); // Output: Hello, my name is Alice
person2.greet(); // Output: Hello, my name is Bob
```

In the above example, the `Person` constructor function has a prototype object that is shared among all instances created from it. We add a `greet` method to the prototype, and all instances of `Person` can access and use this method.

Prototype-based inheritance allows objects to inherit properties and methods from their prototypes, providing a mechanism for code reuse and object composition in JavaScript.

[[^]](#jsinterview)

## Different ways to create objects in js

There are several ways to create objects in JavaScript. Let's explore some of the common methods:

1. Object Literal:

   ```javascript
   const obj = {
     property1: value1,
     property2: value2,
     method: function () {
       // method implementation
     },
   };
   ```

2. Constructor Function:

   ```javascript
   function Person(name, age) {
     this.name = name;
     this.age = age;
     this.greet = function () {
       console.log("Hello, my name is " + this.name);
     };
   }

   const person = new Person("Alice", 25);
   ```

3. Object.create():

   ```javascript
   const obj = Object.create(proto);
   ```

4. Class (Introduced in ECMAScript 2015):

   ```javascript
   class Person {
     constructor(name, age) {
       this.name = name;
       this.age = age;
     }
     greet() {
       console.log("Hello, my name is " + this.name);
     }
   }

   const person = new Person("Alice", 25);
   ```

5. Factory Function:

   ```javascript
   function createPerson(name, age) {
     return {
       name: name,
       age: age,
       greet: function () {
         console.log("Hello, my name is " + this.name);
       },
     };
   }

   const person = createPerson("Alice", 25);
   ```

6. Object Constructor:
   ```javascript
   const obj = new Object();
   obj.property = value;
   obj.method = function () {
     // method implementation
   };
   ```

These are just a few of the common ways to create objects in JavaScript. Each method has its own advantages and use cases. The choice of which method to use depends on the specific requirements of your code and the design patterns you follow.

[[^]](#jsinterview)

## First class function and Pure function in js

1. First-Class Functions:
   In JavaScript, functions are considered first-class citizens, which means they can be treated like any other value. This enables functions to be assigned to variables, passed as arguments to other functions, returned from functions, and stored in data structures. Key features of first-class functions include:

- Functions can be assigned to variables:

  ```javascript
  const add = function (a, b) {
    return a + b;
  };
  ```

- Functions can be passed as arguments to other functions:

  ```javascript
  function performOperation(operation, a, b) {
    return operation(a, b);
  }

  const result = performOperation(add, 5, 3);
  ```

- Functions can be returned from other functions:

  ```javascript
  function createMultiplier(factor) {
    return function (number) {
      return number * factor;
    };
  }

  const double = createMultiplier(2);
  const result = double(5); // Output: 10
  ```

2. Pure Functions:
   A pure function is a function that, given the same input, will always produce the same output and has no side effects. The key characteristics of pure functions are:

- The function's return value solely depends on its arguments:

  ```javascript
  function add(a, b) {
    return a + b;
  }
  ```

- Pure functions do not modify or rely on any external state:

  ```javascript
  const x = 5;

  function multiplyByX(number) {
    return number * x;
  }
  ```

- Pure functions have no side effects (e.g., modifying external variables, modifying DOM, making network requests):
  ```javascript
  function square(number) {
    return number * number;
  }
  ```

Pure functions are deterministic and easier to reason about since they have no hidden dependencies or external state. They facilitate code that is easier to test, debug, and maintain.

[[^]](#jsinterview)

## Curring in js

Currying is a technique in JavaScript where a function with multiple arguments is transformed into a sequence of functions, each taking a single argument. It allows you to partially apply a function by providing only a subset of its arguments, returning a new function that expects the remaining arguments. This technique is named after the mathematician Haskell Curry.

Here's an example to illustrate currying in JavaScript:

```javascript
function multiply(a) {
  return function (b) {
    return a * b;
  };
}

const multiplyByTwo = multiply(2);
const result = multiplyByTwo(5); // Output: 10
```

It can be written as

```js
function multiply(a) {
  return function (b) {
    return a * b;
  };
}

multiply(2)(5); // output: 10
```

In this example, the `multiply` function takes a single argument `a` and returns a new function that takes another argument `b` and performs the multiplication. By calling `multiply(2)`, we create a new function `multiplyByTwo` that multiplies its argument by 2. When we call `multiplyByTwo(5)`, it multiplies 5 by 2 and returns the result of 10.

Currying allows you to create specialized functions from a more general function by fixing some of its arguments in advance. This can be useful in scenarios where you have a function that takes multiple arguments, but you often need to reuse it with some of the arguments predefined.

Currying can be achieved using various techniques in JavaScript, including manual function composition, using libraries like Lodash or Ramda, or leveraging language features like arrow functions and closures.

Note that not all functions need to be curried, and it depends on the specific use case and programming style. Currying can enhance code reusability, functional composition, and make it easier to create specialized versions of functions.

[[^]](#jsinterview)

## Event capturing and events bubbling in js

The default behavior in JavaScript is event bubbling, not event capturing. The event flows from the target element to its ancestors during the bubbling phase by default.

Event Capturing (or Capture Phase):

- Event capturing is the first phase of event propagation.
- During the capture phase, the event traverses through the DOM from the top (outermost ancestor) down to the target element.
- If an event listener is registered to an element during the capture phase, it will be triggered during this phase.
- The capture phase is less commonly used in practice, as the majority of event handling occurs during the bubbling phase.

```html
<div #grandparent>
  <div #parent>
    <div #child></p>
  </div>
</form>
```

```js
const grandParent = document.getElementById("grandparent");
const parent = document.getElementById("parent");
const child = document.getElementById("child");

// Changing value of capture parameter as 'true'
grandParent.addEventListener(
  "click",
  (e) => {
    console.log("GrandParent");
  },
  { capture: true }
);
parent.addEventListener(
  "click",
  (e) => {
    console.log("Parent");
  },
  { capture: true }
);
child.addEventListener(
  "click",
  (e) => {
    console.log("Child");
  },
  { capture: true }
);
```

Event Bubbling (or Bubbling Phase):

- Event bubbling is the second phase of event propagation.
- After the capture phase, during the bubbling phase, the event travels from the target element back up the DOM through its ancestors.
- If an event listener is registered to an element during the bubbling phase, it will be triggered during this phase.
- Event bubbling is the default behavior in most cases and is more widely used.

```html
<div #grandparent>
  <div #parent>
    <div #child></p>
  </div>
</form>
```

```js
const grandParent = document.getElementById("grandparent");
const parent = document.getElementById("parent");
const child = document.getElementById("child");

grandParent.addEventListener(
  "click",
  (e) => {
    console.log("GrandParent");
  },
  { capture: false }
);
parent.addEventListener(
  "click",
  (e) => {
    console.log("Parent");
  },
  { capture: false }
);
child.addEventListener(
  "click",
  (e) => {
    console.log("Child");
  },
  { capture: false }
);
```

[[^]](#jsinterview)

## Synchronous amd asynchronous functions in js

1. Synchronous Functions:

   - Synchronous functions execute in a sequential manner, blocking the execution of subsequent code until they complete.
   - They operate in a single-threaded manner, meaning that each function must complete its task before the next function is executed.
   - Synchronous functions are predictable and deterministic, as their order of execution is guaranteed.
   - Examples of synchronous operations include basic arithmetic calculations, looping through arrays, or executing sequential statements.

2. Asynchronous Functions:
   - Asynchronous functions do not block the execution of subsequent code. Instead, they allow other code to run while they perform their tasks.
   - They typically involve operations that take time to complete, such as fetching data from an external API, reading from a file, or making network requests.
   - Asynchronous functions usually provide a callback function, use Promises, or utilize async/await syntax to handle the result of the operation once it completes.
   - Asynchronous functions allow non-blocking execution, enabling other parts of the program to continue running while waiting for the asynchronous task to finish.
   - Examples of asynchronous operations include setTimeout(), setInterval(), AJAX requests, and file I/O operations.

Asynchronous functions are crucial in scenarios where you need to perform operations that involve waiting for external resources or time-consuming tasks. They help prevent blocking the user interface (UI) and allow for concurrent execution of multiple operations.

Here's an example showcasing the difference between synchronous and asynchronous functions:

```javascript
// Synchronous function
function synchronousTask() {
  console.log("Start");
  for (let i = 0; i < 1000000000; i++) {
    // Time-consuming operation
  }
  console.log("End");
}

// Asynchronous function
function asynchronousTask() {
  console.log("Start");
  setTimeout(function () {
    console.log("Async Task Complete");
  }, 2000);
  console.log("End");
}

// Synchronous function call
synchronousTask();

// Asynchronous function call
asynchronousTask();
```

In this example, the synchronousTask() function performs a time-consuming loop and blocks the subsequent code until it completes. On the other hand, the asynchronousTask() function initiates a setTimeout() operation and immediately moves to the next line without waiting for the setTimeout() delay. The setTimeout() callback function is executed asynchronously after a delay of 2000 milliseconds.

Understanding the distinction between synchronous and asynchronous functions is crucial for managing time-consuming operations, handling I/O operations, and writing efficient code in JavaScript.

[[^]](#jsinterview)

## Why is fetch the preferred way to send a network request via the web browser in js

The `fetch()` function is commonly preferred for sending network requests in JavaScript because it provides a more modern and flexible approach compared to older methods like XMLHttpRequest (XHR). Here are some reasons why `fetch()` is favored:

1. Simplicity and Clarity: The `fetch()` API has a simpler and more intuitive syntax compared to XHR. It uses a promise-based approach, allowing you to chain methods and handle responses in a more straightforward manner.

2. Promise-Based: `fetch()` returns a Promise, making it easier to handle asynchronous operations and work with the response data using methods like `.then()` and `.catch()`. This enables a more elegant way to handle success and error scenarios.

3. Fetch API: `fetch()` is part of the Fetch API, which provides a standardized way to make HTTP requests. It supports various request and response types, including JSON, text, and blobs, and allows you to set headers, specify request methods, and work with cookies.

4. Cross-Origin Resource Sharing (CORS): `fetch()` follows the CORS protocol by default. It allows you to make requests to different domains, enabling cross-origin communication while enforcing security measures.

5. Modern Web Standards: `fetch()` aligns with modern web development standards and integrates well with other APIs. It plays nicely with features like Promises, async/await, and the overall ecosystem of JavaScript libraries and frameworks.

6. Browser Support: `fetch()` enjoys widespread support among modern browsers, including Chrome, Firefox, Safari, and Edge. It is also available in Node.js through third-party libraries like node-fetch.

While `fetch()` is the preferred method for many scenarios, it's important to note that older browsers may not support it. In such cases, you can consider using a polyfill or fallback options like XHR or third-party libraries that provide abstraction layers over network requests.

It's worth mentioning that the `fetch()` API has some considerations and limitations, such as lack of built-in support for handling request cancellation and progress events. However, the JavaScript community has developed various libraries and utilities to address these limitations and provide additional features on top of `fetch()`.

Overall, the `fetch()` API is widely adopted due to its simplicity, standardization, and compatibility with modern JavaScript practices, making it the preferred method for sending network requests in web browsers.

[[^]](#jsinterview)

## Is there another option, besides explicit promises, to handle asynchronous code in JavaScript?

1. Callback Functions: Callback functions have been widely used to handle asynchronous operations in JavaScript before Promises became prevalent. With this approach, you pass a function as an argument to an asynchronous operation, and once the operation completes, the callback function is invoked. However, callback-based code can become complex and lead to callback hell when dealing with multiple asynchronous operations.

2. Async/Await: Introduced in ECMAScript 2017 (ES8), the async/await syntax provides a more readable and concise way to handle asynchronous code. It allows you to write asynchronous code that looks and behaves like synchronous code. The `async` keyword is used to define a function that returns a Promise, and the `await` keyword is used to pause the execution of the function until a Promise is resolved or rejected. This approach simplifies the handling of Promises and reduces the need for explicit `.then()` and `.catch()` chaining.

3. Generators and Yield: Generators, denoted by the function\* syntax, can be used in conjunction with the `yield` keyword to handle asynchronous code in a more sequential manner. By yielding Promises from a generator function, you can pause and resume the execution of the function at specific points. External libraries like `co` or language features like async generators provide ways to work with generators for asynchronous code.

4. Observables: Reactive programming with Observables is another approach to handle asynchronous code. Libraries like RxJS provide the Observable pattern, where you can create streams of asynchronous events and apply transformations and operators to handle those events. Observables allow for powerful event composition, error handling, and cancellation capabilities.

5. Async Library or Framework: There are various third-party libraries and frameworks, such as Async.js or Bluebird, that offer utilities and abstractions for handling asynchronous code. These libraries provide features like parallel execution, control flow, and error handling mechanisms to simplify asynchronous programming.

While Promises are now a standard part of JavaScript and the most widely supported approach for handling asynchronous code, the alternatives mentioned above can still be useful in specific scenarios or for compatibility with older codebases. It's important to consider the specific requirements of your project and the level of browser or platform support when choosing the best approach for handling asynchronous code.

[[^]](#jsinterview)

## What are the differences between arrow functions and function expressions

Arrow functions and function expressions are both ways to define functions in JavaScript, but they differ in syntax and behavior. Here are the key differences between arrow functions and function expressions:

1. Syntax:

   - Arrow Function Syntax: Arrow functions have a concise syntax using the `=>` (fat arrow) operator. They are defined as `(parameters) => { ... }` or `(parameters) => expression`.
   - Function Expression Syntax: Function expressions are defined using the `function` keyword, followed by an optional function name, a set of parameters in parentheses, and a function body enclosed in curly braces.

2. Lexical `this` Binding:

   - Arrow Functions: Arrow functions do not have their own `this` context. Instead, they lexically bind `this` to the enclosing scope, meaning they inherit the `this` value from the surrounding code. This behavior can be useful when working with callbacks or nested functions, as it avoids potential confusion with the `this` value.
   - Function Expressions: Function expressions have their own `this` context, which is determined by how the function is invoked. The value of `this` can change depending on how the function is called or if it is bound explicitly using `bind()`, `call()`, or `apply()`.

3. Arguments Object:

   - Arrow Functions: Arrow functions do not have their own `arguments` object. The `arguments` object refers to the arguments passed to the enclosing non-arrow function.
   - Function Expressions: Function expressions have their own `arguments` object, which provides access to the arguments passed to the function itself.

4. `new` Operator:

   - Arrow Functions: Arrow functions cannot be used as constructors with the `new` operator. Attempting to do so will result in a runtime error.
   - Function Expressions: Function expressions can be used as constructors with the `new` operator to create new instances of objects. The `this` value within the function refers to the newly created object.

5. Binding of `this` in Methods:

   - Arrow Functions: Arrow functions are not suitable for use as object methods when you need to access the object's properties or methods using `this`. Since arrow functions don't have their own `this`, `this` will refer to the surrounding scope, which is usually not the object itself.
   - Function Expressions: Function expressions can be used as methods in objects, and `this` within the function refers to the object itself.

6. Availability of `arguments.callee`:
   - Arrow Functions: Arrow functions do not have access to `arguments.callee`, which refers to the currently executing function. Attempts to use `arguments.callee` within an arrow function will result in a runtime error.
   - Function Expressions: Function expressions can access `arguments.callee` to refer to the currently executing function.

Overall, arrow functions are more concise and have a different behavior for `this` and `arguments` compared to function expressions. They are often used for shorter, anonymous functions and in situations where you want to preserve the surrounding scope's `this` value. Function expressions, on the other hand, provide more flexibility and have a separate `this` context, making them suitable for a wider range of use cases, including object methods, constructors, and functions that require access to `arguments.callee`.

```js
// Arrow Function
const arrowFunc = (x, y) => {
  console.log(this); // `this` is inherited from the surrounding context
  console.log(x + y);
};

arrowFunc(2, 3); // Output: 5

// Function Expression
const funcExpr = function (x, y) {
  console.log(this); // `this` refers to the current context
  console.log(x + y);
};

funcExpr(2, 3); // Output: 5
```

[[^]](#jsinterview)

## What is the difference between a type and an interface in TypeScript?

In TypeScript, both types and interfaces are used to define the shape and structure of objects and provide type annotations. However, there are some differences between them in terms of their features and usage.

Here are some key differences between types and interfaces in TypeScript:

1. Syntax: The syntax for defining types and interfaces is different. Types are defined using the `type` keyword, while interfaces are defined using the `interface` keyword.

2. Extensibility: Interfaces can be extended to create new interfaces using the `extends` keyword, allowing for the composition of multiple interfaces. On the other hand, types cannot be extended directly; they can only be combined using intersection (`&`) or union (`|`) operators.

3. Declaration Merging: Interfaces support declaration merging, which means that multiple interface declarations with the same name are merged into a single interface definition. This allows you to add or modify properties and methods of an existing interface. Types do not support declaration merging.

4. Compatibility: Interfaces are open-ended, meaning they can be implemented by objects that have more properties than the ones defined in the interface. Types, on the other hand, are exact and do not allow additional properties. This makes types more suitable for describing the exact shape of an object.

5. Union and Intersection: Types are more flexible when it comes to working with union (`|`) and intersection (`&`) types. Types can be easily combined using these operators, allowing for more complex type definitions. Interfaces have limited support for union and intersection types.

```js
// Example using type
type PersonType = {
  name: string,
  age: number,
  greet: () => void,
};

const person1: PersonType = {
  name: "John",
  age: 25,
  greet: () => {
    console.log(
      `Hello, my name is ${person1.name} and I am ${person1.age} years old.`
    );
  },
};

person1.greet(); // Output: Hello, my name is John and I am 25 years old.

// Example using interface
interface PersonInterface {
  name: string;
  age: number;
  greet(): void;
}

const person2: PersonInterface = {
  name: "Alice",
  age: 30,
  greet() {
    console.log(
      `Hello, my name is ${person2.name} and I am ${person2.age} years old.`
    );
  },
};

person2.greet(); // Output: Hello, my name is Alice and I am 30 years old.

// Extending Interface
interface Shape {
  color: string;
}

interface Square extends Shape {
  sideLength: number;
}

const square: Square = {
  color: "red",
  sideLength: 5,
};

console.log(square.color); // Output: red
console.log(square.sideLength); // Output: 5

// Union and Intersection on Type
type Pet = { name: string };
type Dog = Pet & { breed: string };
type Cat = Pet & { color: string };

const dog: Dog = { name: "Buddy", breed: "Labrador" };
const cat: Cat = { name: "Whiskers", color: "gray" };

console.log(dog.name); // Output: Buddy
console.log(dog.breed); // Output: Labrador

console.log(cat.name); // Output: Whiskers
console.log(cat.color); // Output: gray

type DogOrCat = Dog | Cat;
const pet: DogOrCat = Math.random() < 0.5 ? dog : cat;

if ("breed" in pet) {
  console.log("Breed: " + pet.breed); // Output: Breed: Labrador
} else if ("color" in pet) {
  console.log("Color: " + pet.color); // Output: Color: gray
}
```

[[^]](#jsinterview)

## What are the five key data structures in js

In JavaScript, there are several key data structures that are commonly used. While there are more than five data structures available, here are five fundamental ones:

1. **Array**: An array is a linear data structure that stores elements in an ordered list. It is capable of holding elements of different types and allows efficient random access to elements using numerical indices. Arrays can dynamically grow or shrink in size.

2. **Object**: An object is an unordered collection of key-value pairs, where each key is unique. It is a versatile data structure that allows storing and accessing values using their associated keys. Objects can hold any type of data, including other objects or functions.

3. **Set**: A set is a collection of unique values, where each value occurs only once. It provides methods for adding, removing, and checking the presence of elements efficiently. Sets are particularly useful when dealing with a collection of distinct values or performing set operations like union, intersection, and difference.

4. **Map**: A map is a data structure that stores key-value pairs, similar to an object. However, it provides additional functionality and guarantees the order of insertion. Maps allow efficient key-based operations like adding, updating, and retrieving values. They are commonly used when the order of elements or the ability to iterate over them in a specific order is important.

5. **Stack**: A stack is a Last-In-First-Out (LIFO) data structure where elements are added and removed from the top. It follows the principle of "last in, first out." Stacks are used in various scenarios, such as managing function calls, undo/redo functionality, and evaluating expressions.

[[^]](#jsinterview)

## Data types in js

1. Primitive Data Types:

   - Number: Represents numeric values, both integers and floating-point numbers.
   - String: Represents textual data enclosed in single quotes ('') or double quotes ("").
   - Boolean: Represents either true or false.
   - Undefined: Represents a variable that has been declared but has not been assigned a value.
   - Null: Represents the intentional absence of any object value.
   - Symbol: Represents a unique identifier that is used primarily as an object property.

2. Object: Represents a collection of key-value pairs or properties. Objects can contain any combination of primitive values, objects, functions, and arrays.

3. Array: Represents an ordered collection of elements enclosed in square brackets ([]). Arrays can contain elements of any data type, including other arrays.

4. Function: Represents a reusable block of code that can be invoked or called with arguments. Functions can take parameters, perform operations, and return values.

5. BigInt: Represents integers with arbitrary precision, enabling the handling of numbers beyond the limitations of the Number data type.

[[^]](#jsinterview)

## What is generics? In typescript

Generics are the fundamental concept of any typed language where you can pass a custom type as a parameter and construct the instance according to that. Generic types give the ability and control to a component to enforce the type on the user.

```js
function functionName<T>(value: T): T {
  return value;
}
```

```js
// Example 1: Reusability
function printArray<T>(arr: T[]): void {
  arr.forEach((item) => console.log(item));
}

const numbers: number[] = [1, 2, 3, 4, 5];
const strings: string[] = ["apple", "banana", "cherry"];

printArray(numbers); // Output: 1 2 3 4 5
printArray(strings); // Output: apple banana cherry

// Example 2: Type Safety
function firstElement<T>(arr: T[]): T {
  return arr[0];
}

const firstNum: number = firstElement(numbers); // Type-safe
console.log(firstNum); // Output: 1

// const firstStr: string = firstElement(numbers); // Type error

// Example 3: Flexibility
interface Box<T> {
  value: T;
}

const numberBox: Box<number> = { value: 10 };
const stringBox: Box<string> = { value: "Hello" };

console.log(numberBox.value); // Output: 10
console.log(stringBox.value); // Output: Hello
```

[[^]](#jsinterview)

## What does closure mean in programming?

1. Access to Outer Variables: A closure enables a function to access variables from its parent scope, even after the parent function has finished executing. This is possible because the inner function maintains a reference to its outer environment.

2. Preservation of State: Closures allow for the preservation of the state of variables. The inner function can still access and manipulate the values of the outer variables, even if the outer function has completed its execution. This feature makes closures useful in scenarios like maintaining private data or creating factories.

3. Lexical Scoping: Closures are based on lexical scoping, where variables are resolved based on their location in the source code. This means that closures capture the values of variables at the time the inner function is defined, not when it is executed.

4. Multiple Closures: Multiple closures can be created within the same scope, each with its own preserved set of variables. Each closure maintains its own unique reference to the outer variables.

Closures are commonly used in JavaScript and other programming languages for various purposes, such as creating private variables, implementing data hiding, handling asynchronous operations, and creating higher-order functions.

Here's an example to illustrate closures in JavaScript:

```javascript
function outerFunction() {
  var outerVariable = "Hello";

  function innerFunction() {
    console.log(outerVariable);
  }

  return innerFunction;
}

var closure = outerFunction();
closure(); // Output: Hello
```

In the above example, the `innerFunction` is defined within the `outerFunction` and has access to the `outerVariable` even after the `outerFunction` has finished executing. The returned `innerFunction` forms a closure that preserves the reference to `outerVariable`, allowing it to be accessed when the closure is invoked.

Closures are a powerful and fundamental concept in programming, providing a way to manage and encapsulate state within functions, leading to more flexible and expressive code.

[[^]](#jsinterview)

## var, let & const in JS

In JavaScript, `var`, `let`, and `const` are used to declare variables. Each of them has a different scope and behavior, and hoisting affects them in distinct ways. Let's go through each of them:

1. `var`: Variables declared with `var` have function scope or global scope, depending on where they are declared. When a function is defined, any variables declared with `var` within that function are hoisted to the top of the function scope. This means that you can access and use `var` variables before they are actually declared in the code. However, if `var` variables are declared outside of any function (i.e., in the global scope), they become properties of the global object (e.g., `window` object in browsers). Hoisting in the case of `var` moves the variable declarations to the top, but the assignments remain in the same place.

2. `let`: Variables declared with `let` have block scope, which means they are only accessible within the block of code where they are defined (enclosed within curly braces `{}`). Unlike `var`, `let` variables are not hoisted to the top of their scope. If you try to access a `let` variable before its declaration, you'll encounter a "ReferenceError". It's important to note that the hoisting of `let` variables is limited to the temporal dead zone (TDZ) — the span of code between the variable's creation and its declaration.

3. `const`: Variables declared with `const` also have block scope like `let`, but they are used to declare constants that cannot be reassigned once they are defined. Like `let`, `const` variables are not hoisted to the top of their scope and are subject to the TDZ. You need to assign a value to a `const` variable at the time of declaration, and subsequent reassignments will result in a "TypeError".

Regarding functions:

The `function` keyword is used to declare traditional functions in JavaScript. Function declarations are hoisted to the top of their scope, so you can call a function before its actual declaration in the code. Function declarations have their own scope, which is either the global scope or the function scope where they are defined. Function declarations also have their own `this` value.

On the other hand, arrow functions (`() => {}`) were introduced in ECMAScript 6 and have a different behavior. Arrow functions do not have their own `this` value. Instead, they inherit the `this` value from the enclosing scope. Additionally, arrow functions do not have their own `arguments` object, but they can access the `arguments` object of the enclosing scope. Arrow functions are not hoisted like function declarations; they need to be defined before they are used.

To summarize, `var` variables are function-scoped or globally scoped and are hoisted to the top of their scope, `let` and `const` variables are block-scoped and are not hoisted in a way that you can use them before their declaration, function declarations are hoisted and have their own scope, and arrow functions have lexical scoping, inherit `this` from the enclosing scope, and are not hoisted.

```js
console.log(x); // Output: undefined
var x = 10;

console.log(y); // ReferenceError: y is not defined
let y = 20;

const z = 30;
z = 40; // TypeError: Assignment to constant variable.

hoistedFunction(); // Output: "I'm a hoisted function!"
function hoistedFunction() {
  console.log("I'm a hoisted function!");
}

nonHoistedFunction(); // TypeError: nonHoistedFunction is not a function
var nonHoistedFunction = function () {
  console.log("I'm not hoisted!");
};

arrowFunction(); // ReferenceError: arrowFunction is not defined
const arrowFunction = () => {
  console.log("I'm an arrow function!");
};
```

In the code above, we have examples of var, let, and const variables, as well as function declarations and arrow functions.

- The var x declaration is hoisted to the top of its scope, so even though the variable is accessed before the declaration, it outputs undefined.

- The let y declaration is not hoisted, so trying to access it before the declaration results in a "ReferenceError".

- The const z declaration is also not hoisted, and since const variables cannot be reassigned, the subsequent assignment to z throws a "TypeError".

- The hoistedFunction is a function declaration, which is hoisted to the top of its scope. Therefore, it can be called before its actual declaration in the code.

- The nonHoistedFunction is assigned to a function expression using var. Since var variables are hoisted but the assignment remains in place, calling nonHoistedFunction before the assignment results in a "TypeError" because it is undefined at that point.

- The arrowFunction is an arrow function assigned to a const variable. Arrow functions are not hoisted, so trying to call arrowFunction before its declaration in the code leads to a "ReferenceError".

[[^]](#jsinterview)

## context & this in jS

In JavaScript, the `this` keyword refers to the current execution context or the object to which a function belongs. The value of `this` is determined dynamically based on how a function is called. Understanding the context and behavior of `this` is crucial for proper function invocation and accessing object properties. Here are some important points to consider:

1. Global Context: In the global scope (outside of any function), `this` refers to the global object. In a browser environment, the global object is `window`, while in Node.js, it is `global`.

2. Function Context: When a function is called as a method of an object, `this` points to the object that owns the method. For example:

```javascript
const person = {
  name: "John",
  greet: function () {
    console.log("Hello, my name is " + this.name);
  },
};

person.greet(); // Output: Hello, my name is John
```

In this case, within the `greet` method, `this` refers to the `person` object.

3. Constructor Context: When a function is used as a constructor with the `new` keyword, `this` refers to the newly created object instance. Constructors are typically defined using function declarations or expressions and are intended to create multiple instances of an object with shared properties and methods. For example:

```javascript
function Person(name) {
  this.name = name;
}

const john = new Person("John");
console.log(john.name); // Output: John
```

Here, `this` inside the `Person` constructor refers to the newly created `Person` object (`john`).

4. Explicit Context: The `this` context can be explicitly set using `call()`, `apply()`, or `bind()` methods, which allow you to specify the value of `this` when calling a function. For example:

```javascript
function greet() {
  console.log("Hello, " + this.name);
}

const person = {
  name: "John",
};

greet.call(person); // Output: Hello, John
```

In this case, `call()` is used to invoke the `greet` function with `this` explicitly set to the `person` object.

5. Arrow Functions Context: Arrow functions have a lexical `this` context, which means that `this` is inherited from the enclosing (parent) scope and does not have its own `this` value. Arrow functions are not suitable for methods that need dynamic context, but they are commonly used in callback functions or for preserving the outer `this` value. For example:

```javascript
const person = {
  name: "John",
  greet: function () {
    setTimeout(() => {
      console.log("Hello, my name is " + this.name);
    }, 1000);
  },
};

person.greet(); // Output (after 1 second): Hello, my name is John
```

In the above code, the arrow function inside the `setTimeout` callback preserves the `this` value from the `greet` method, allowing it to access the `name` property of the `person` object.

Understanding the context and behavior of `this` is essential for proper JavaScript programming, as it determines how functions interact with objects and enables dynamic behavior based on the execution context.

---

```js
const obj = {
  a: this,
  b: function () {
    return this;
  },
  c: () => {
    return this;
  },
  d() {
    return this;
  },
  e: function () {
    return this.a;
  },
};
```

Certainly! Let's consider an improved example to illustrate the different contexts of the `this` keyword within the `obj` object:

```javascript
const obj = {
  a: this,
  b: function () {
    return this;
  },
  c: () => {
    return this;
  },
  d() {
    return this;
  },
  e: function () {
    return this.a;
  },
};

console.log(obj.a); // Output: [object Window] (Referring to the global object)
console.log(obj.b()); // Output: {b: ƒ, d: ƒ, e: ƒ} (Referring to the object 'obj')
console.log(obj.c()); // Output: [object Window] (Referring to the global object)
console.log(obj.d()); // Output: {b: ƒ, d: ƒ, e: ƒ} (Referring to the object 'obj')
console.log(obj.e()); // Output: undefined (Referring to the 'a' property of 'undefined')
```

In this example, the behavior of `this` can be observed as follows:

1. Property `a: this`: When `obj.a` is accessed, `this` refers to the global object (`[object Window]` in a browser environment). This happens because the object literal does not have its own scope, and therefore `this` in this context points to the global object.

2. Method `b: function() {...}`: When `obj.b()` is called, `this` inside the function refers to the object `obj`. It returns the object `obj` itself (`{b: ƒ, d: ƒ, e: ƒ}`) since `this` is bound to the object it is called upon.

3. Property `c: () => {...}` (Arrow function): In this case, the arrow function captures the `this` value from the surrounding (lexical) scope, which is the global object. Hence, calling `obj.c()` returns the global object (`[object Window]`).

4. Method `d() {...}` (Shorthand method): Similar to method `b`, the shorthand method `d` also has `this` bound to the object `obj` when `obj.d()` is called. Therefore, it returns the object `obj` itself (`{b: ƒ, d: ƒ, e: ƒ}`).

5. Method `e: function() {...}`: Inside the `e` method, `this.a` is used to access the `a` property of the object `obj`. However, since `obj.e()` is called from within `obj` itself, `this` inside `obj.e()` refers to the object `obj`. However, the object `obj` does not have a property `a`, so it returns `undefined`.

By analyzing the output of each console.log statement, we can observe the different values of `this` depending on the context in which it is used within the `obj` object.

[[^]](#jsinterview)

## Diff btw .map &.forEach in js

`forEach` and `map` are both array methods in JavaScript, used for iterating over elements in an array. However, they have some differences in terms of their purpose and the return values they provide.

1. Purpose:

   - `forEach`: The `forEach` method is used to execute a provided callback function once for each element in an array. It is mainly used for performing side effects, such as modifying the array, updating external variables, or logging values.
   - `map`: The `map` method, on the other hand, is used to create a new array by applying a transformation function to each element of the original array. It is specifically designed to generate a new array based on the modified values from the original array, without modifying the original array itself.

2. Return Value:

   - `forEach`: The `forEach` method does not return a new array. It simply iterates over each element in the array and executes the provided callback function. The return value of the `forEach` method is always `undefined`.
   - `map`: The `map` method returns a new array containing the results of applying the provided callback function to each element of the original array. It creates a transformed array with the same length as the original array.

3. Usage and Effects:
   - `forEach`: Since the primary purpose of `forEach` is to perform side effects, such as modifying the array or updating external variables, it is commonly used when you want to iterate over an array and perform some action on each element. It is suitable for scenarios where you don't need a new array as the result.
   - `map`: The primary purpose of `map` is to transform each element of an array and create a new array based on the transformations. It is often used when you need to transform data or extract specific properties from the original array to generate a new array.

Here's an example to illustrate the difference between `forEach` and `map`:

```javascript
const numbers = [1, 2, 3, 4, 5];

// Using forEach
numbers.forEach((num) => {
  console.log(num * 2); // Side effect: Logging the doubled value
});
// Output: 2, 4, 6, 8, 10
// Return value: undefined

// Using map
const doubledNumbers = numbers.map((num) => {
  return num * 2; // Transformation: Doubling each number
});
console.log(doubledNumbers);
// Output: [2, 4, 6, 8, 10]
// Return value: [2, 4, 6, 8, 10]
```

[[^]](#jsinterview)

## macro, micro & event loop

Certainly! Here's a short explanation with code:

```javascript
console.log("Start");

setTimeout(() => {
  console.log("Timeout");
}, 0);

Promise.resolve().then(() => {
  console.log("Promise");
});

console.log("End");
```

In this code, we have a mix of macro and micro tasks:

1. `console.log('Start')`: This is a regular synchronous code that executes immediately and logs "Start" to the console.

2. `setTimeout(() => {...}, 0)`: This represents a macro task, a timer event in this case. Even though the delay is set to 0 milliseconds, it is still considered a macro task. The callback function will be executed by the event loop after the current stack is empty. Therefore, it will be logged after other synchronous code.

3. `Promise.resolve().then(() => {...})`: This represents a micro task. The `Promise.resolve()` creates a resolved promise, and the attached `then` callback is a micro task. Micro tasks have a higher priority than macro tasks and are executed before the next rendering or input event. Therefore, the callback function will be executed before the macro task. It will log "Promise" to the console.

4. `console.log('End')`: This is another synchronous code that logs "End" to the console.

Expected Output:

```
Start
End
Promise
Timeout
```

The order of execution is as follows:

- Synchronous code is executed first, so "Start" and "End" are logged to the console.
- Micro tasks are processed before the next rendering or input event, so the micro task callback for the resolved promise is executed, logging "Promise" to the console.
- Finally, the macro task callback inside the `setTimeout` is executed, logging "Timeout" to the console.

This demonstrates the event loop's behavior, where micro tasks are processed before macro tasks, allowing for efficient handling of both high-priority operations (micro tasks) and lower-priority operations (macro tasks).

---

```javascript
console.log(1);
setTimeout(() => console.log(2), 0);
Promise.resolve().then(() => console.log(3));
setTimeout(() => console.log(4), 1);
console.log(5);
```

Explanation:

1. `console.log(1)`: This is a synchronous code that logs `1` to the console immediately.

2. `setTimeout(() => console.log(2), 0)`: This represents a macro task, a timer event with a delay of 0 milliseconds. Even though the delay is set to 0, the callback function is still considered a macro task. It will be queued in the task queue and executed by the event loop after the current stack is empty.

3. `Promise.resolve().then(() => console.log(3))`: This represents a micro task. The `Promise.resolve()` creates a resolved promise, and the attached `then` callback is a micro task. Micro tasks have a higher priority than macro tasks and are executed before the next rendering or input event. The micro task callback will be executed before the next macro task.

4. `setTimeout(() => console.log(4), 1)`: This is another macro task, a timer event with a delay of 1 millisecond. The callback function will be queued in the task queue and executed after the current stack is empty and at least 1 millisecond has passed.

5. `console.log(5)`: This is a synchronous code that logs `5` to the console immediately.

Expected Output:

```
1
5
3
2
4
```

Explanation of the output:

- Synchronous code is executed first, so `1` is logged to the console.
- Then, `setTimeout(() => console.log(2), 0)` is encountered. It is a macro task, so it is queued in the task queue.
- `Promise.resolve().then(() => console.log(3))` is a micro task, which is executed before the next macro task. So, `3` is logged to the console.
- Next, `console.log(5)` is executed, logging `5` to the console.
- Now, the event loop moves to the task queue and executes the first macro task, which is `setTimeout(() => console.log(2), 0)`. Hence, `2` is logged to the console.
- Finally, the last macro task `setTimeout(() => console.log(4), 1)` is executed, and `4` is logged to the console.

This order of execution demonstrates the event loop behavior, where micro tasks are executed before the next macro task, even if they were enqueued later.

[[^]](#jsinterview)

## Deep copy via recursion

```js
function deepCopy(obj) {
  if (obj === null || typeof obj !== "object") {
    return obj;
  }

  let copy = Array.isArray(obj) ? [] : {};

  for (let key in obj) {
    if (obj.hasOwnProperty(key)) {
      copy[key] = deepCopy(obj[key]);
    }
  }

  return copy;
}

const obj = {
  a: 1,
  b: "hello",
  c: {
    d: "world",
  },
  e: {
    f: {
      g: 100,
    },
  },
};

const deepCopyObj = deepCopy(obj);
```
