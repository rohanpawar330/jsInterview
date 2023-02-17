# jsInterview

* [HTTP vs HTTPS](#http-vs-https)
* [Http methods](#http-methods)
* [Javascript is single-threaded](#javascript-is-single-threaded)
* [web-workers](#web-workers)
* [null vs undefined](#null-vs-undefined)
* [Put vs Post http request](#put-vs-post-http-request)
* [call, apply & bind](#call-apply--bind)
* [SOLID principals in js](#solid-principals-in-js)
* [jit & aot](#jit--aot)
* [ProvidedIn in Angular](#providerin-in-angular)
* [Change detection in angular](#change-detection-in-angular)
* [Encapsulation](#encapsulation)
* [Directive & Component & Pipes](#directive--component--pipes)

[[^]](#jsinterview)
## js work 


[[^]](#jsinterview)
## http vs https 

<b>HTTP vs HTTPS</b> : HTTP stands for Hypertext Transfer Protocol,used for transferring data over a network. Most information that is sent over the Internet, including website content and API calls, uses the HTTP protocol. 
An HTTP request is just a series of lines of text that follow the HTTP protocol. A GET request might look like
```
GET /hello.txt HTTP/1.1
User-Agent: curl/7.63.0 libcurl/7.63.0 OpenSSL/1.1.l zlib/1.2.11
Host: www.example.com
Accept-Language: en
```

This is especially an issue when users submit sensitive data via a website or a web application. This could be a password, a credit card number, or any other data entered into a form, and in HTTP all this data is sent in plaintext for anyone to read.

If a website uses HTTP instead of HTTPS, all requests and responses can be read by anyone who is monitoring the session.

The S in HTTPS stands for "secure." HTTPS uses TLS (or SSL) to encrypt HTTP requests and responses, so in the example above, instead of the text, an attacker would see a bunch of seemingly random characters.

Instead of:


```
GET /hello.txt HTTP/1.1
User-Agent: curl/7.63.0 libcurl/7.63.0 OpenSSL/1.1.l zlib/1.2.11
Host: www.example.com
Accept-Language: en
```

The attacker sees something like:

```
t8Fw6T8UV81pQfyhDkhebbz7+oiwldr1j2gHBB3L3R
```
`TLS` uses a technology called public key `cryptography`: there are two keys, a public key and a private key, and the public key is shared with client devices via the server's SSL certificate. When a client opens a connection with a server, the two devices use the public and private key to agree on new keys, called session keys, to encrypt further communications between them.

All HTTP requests and responses are then encrypted with these session keys, so that anyone who intercepts communications can only see a random string of characters, not the plaintext

This prevents or helps block a number of attacks that are possible when there is no authentication, such as:

* On-path attacks
* DNS hijacking
* BGP hijacking
* Domain spoofing

[[^]](#jsinterview)
## Javascript is single-threaded 

_JavaScript_ is called a ***"single-threaded"*** language because it can only execute one piece of code at a time. This means that if one function is running, it has to finish before another function can start.

JavaScript has a single `call stack`, which is a data structure used by the JavaScript engine to keep track of which functions are currently running and in what order. 

JavaScript code must be written in a way that avoids long-running or blocking operations, as these can cause the user interface to freeze and become unresponsive.

JavaScript is single-threaded, it can still make use of asynchronous operations like _callbacks, promises, and async/await_ to handle multiple tasks without blocking the main thread. Additionally, modern web browsers have introduced Web Workers, which allow JavaScript code to run in separate threads for heavy computation, but these are still relatively limited in use.

[[^]](#jsinterview)
## web-workers 

Web Workers are a browser feature that allows you to run JavaScript code in a separate background thread from the main UI thread of the web page. This means that you can execute heavy, long-running JavaScript code in the background, without blocking the user interface and making the web page unresponsive.

Web Workers were introduced in HTML5 and are supported in most modern web browsers, including Chrome, Firefox, Safari, and Edge. They work by creating a new thread in the browser's JavaScript engine, which can execute scripts independently of the main UI thread.

```
// main.js

// create a new Web Worker
const worker = new Worker('worker.js');

// send a message to the worker
worker.postMessage('Hello from the main thread!');

// listen for messages from the worker
worker.onmessage = function(event) {
  console.log('Received message from worker:', event.data);
};

// worker.js

// listen for messages from the main thread
onmessage = function(event) {
  console.log('Received message from main thread:', event.data);

  // perform a long-running task
  const result = performLongRunningTask();

  // send the result back to the main thread
  postMessage(result);
};

function performLongRunningTask() {
  // simulate a long-running task
  let sum = 0;
  for (let i = 0; i < 1000000000; i++) {
    sum += i;
  }
  return sum;
}

```

[[^]](#jsinterview)
## null vs undefined 

**null** and **undefined** are both special values that represent absence of a value, but they are not the same thing.

undefined is a primitive value that is automatically assigned to a variable that has been declared but has not been assigned a value, or to a function argument that has not been passed a value. It can also be explicitly assigned to a variable, indicating the intentional absence of a value.

For example:
```
let x; // variable x is undefined
console.log(x); // output: undefined

function foo(y) {
  console.log(y); // output: undefined
}

foo(); // calling function foo with no arguments
```

null, on the other hand, is a special value that represents the intentional absence of any object value. It is typically used as a way of indicating that a variable should have no value or that an object property should be empty.

For example:
```let x = null; // variable x has no value
console.log(x); // output: null

let obj = {
  prop1: "value1",
  prop2: null
};
console.log(obj.prop2); // output: null
```

**It's important to note that null is an object in JavaScript, whereas undefined is a primitive value. This means that null can be assigned to an object, but not to a primitive type like a number or a string.

[[^]](#jsinterview)
## Http methods 

HTTP (Hypertext Transfer Protocol) is a protocol used for communication between web servers and web clients (such as browsers). HTTP defines a set of methods, also known as verbs, that indicate the action to be performed on the specified resource. The most common HTTP methods are:

1. GET: retrieves a resource (such as a web page or an image) from the server.
2. POST: submits data (such as form data) to be processed by the server.
3. PUT: updates an existing resource on the server.
4. DELETE: deletes a resource from the server.
5. HEAD: retrieves only the headers of a resource, without the body content.
6. OPTIONS: retrieves the supported methods for a resource.
7. CONNECT: establishes a network connection to a resource, usually for use with HTTPS.
8. TRACE: retrieves a diagnostic trace of the actions performed by the server on a request.
9. PATCH: partially updates an existing resource on the server.

Each HTTP method has a specific set of rules and restrictions for how it should be used, and each method is associated with a specific set of status codes that indicate the outcome of the request. For example, a successful GET request typically results in a 200 OK status code, while a failed POST request might result in a 400 Bad Request or 500 Internal Server Error status code, depending on the nature of the error.

[[^]](#jsinterview)
## Put vs Post http request 

PUT and POST are both HTTP methods used to send data to a server in JavaScript and other programming languages, but they have different purposes and usage.

The main difference between PUT and POST is that PUT is used to update an existing resource, while POST is used to create a new resource.

Here is an example of a PUT request in JavaScript:
```const data = { title: 'Updated post', body: 'This is an updated post' };

fetch('https://jsonplaceholder.typicode.com/posts/1', {
  method: 'PUT',
  headers: {
    'Content-Type': 'application/json'
  },
  body: JSON.stringify(data)
})
  .then(response => response.json())
  .then(data => console.log(data));
```

In this example, we are updating the first post on the jsonplaceholder API using a PUT request. The headers and body options are used to send JSON data to the server with the updated post data.

And here is an example of a POST request in JavaScript:

```
const data = { title: 'New post', body: 'This is a new post' };

fetch('https://jsonplaceholder.typicode.com/posts', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json'
  },
  body: JSON.stringify(data)
})
  .then(response => response.json())
  .then(data => console.log(data));
```

In this example, we are creating a new post on the jsonplaceholder API using a POST request. The headers and body options are used to send JSON data to the server with the new post data.

In general, you should use PUT when you want to update an existing resource, and use POST when you want to create a new resource. 

[[^]](#jsinterview)
## call, apply & bind 


call, bind, and apply are three methods available on JavaScript function objects, which allow you to call or apply a function with a specific this value and arguments.


Here are some scenarios where you might use call, bind, or apply:

1. Changing the this value of a function: When you call a function in JavaScript, the value of this is set to the context of the function call. However, sometimes you might want to change the this value of a function to a specific object. In this case, you can use call, bind, or apply.

2. Passing arguments to a function: Sometimes you might want to pass arguments to a function dynamically, rather than hard-coding them in the function definition. In this case, you can use call, bind, or apply to pass arguments to a function as an array or individual arguments.

3. Creating a new function with a specific this value: When you use bind on a function, it returns a new function with the this value set to a specific object. This can be useful when you want to create a new function with a fixed this value that you can reuse later.

4. Method borrowing: You can use call to borrow a method from one object and use it on another object. This can be useful when you have two objects with similar methods but different properties.

5. Function currying: Function currying is the technique of creating a new function by binding some arguments to a function, so that it can be called with fewer arguments later. This can be done using bind.

Overall, call, bind, and apply are powerful tools in JavaScript that allow you to change the this value of a function and pass arguments dynamically. They are particularly useful when working with functions that have flexible arguments and/or need to be called in different contexts.

1. Changing the this value of a function:

```
const person = {
  name: 'John',
  age: 30
};

function sayHello() {
  console.log(`Hello, my name is ${this.name} and I'm ${this.age} years old.`);
}

// Using call to invoke sayHello with person as the 'this' value
sayHello.call(person); // Output: Hello, my name is John and I'm 30 years old.

// Using apply to invoke sayHello with person as the 'this' value
sayHello.apply(person); // Output: Hello, my name is John and I'm 30 years old.

// Using bind to create a new function with person as the 'this' value
const johnSaysHello = sayHello.bind(person);
johnSaysHello(); // Output: Hello, my name is John and I'm 30 years old.
```

2. Passing arguments to a function:

```
function saySkills(skills) {
  console.log(`My skills are ${skills.join(', ')}.`);
}

// Using call to pass arguments as individual values
saySkills.call(null, 'JavaScript', 'HTML', 'CSS'); // Output: My skills are JavaScript, HTML, CSS.

// Using apply to pass arguments as an array
saySkills.apply(null, [['JavaScript', 'HTML', 'CSS']]); // Output: My skills are JavaScript, HTML, CSS.

// Using bind to create a new function with arguments bound
const logSkills = saySkills.bind(null, ['JavaScript', 'HTML', 'CSS']);
logSkills(); // Output: My skills are JavaScript, HTML, CSS.

```
3. Creating a new function with a specific this value:

```
const person = {
  name: 'John',
  age: 30
};

function sayHello() {
  console.log(`Hello, my name is ${this.name} and I'm ${this.age} years old.`);
}

// Using bind to create a new function with person as the 'this' value
const johnSaysHello = sayHello.bind(person);
johnSaysHello(); // Output: Hello, my name is John and I'm 30 years old.

```

4. Method borrowing:
```
const cat = {
  name: 'Mittens',
  meow: function() {
    console.log(`${this.name} says "meow!"`);
  }
};

const dog = {
  name: 'Rover'
};

// Using call to borrow the meow method from cat and call it with dog as the 'this' value
cat.meow.call(dog); // Output: Rover says "meow!"

```
5. Function currying:

```
function multiply(x, y) {
  return x * y;
}

const multiplyByTwo = multiply.bind(null, 2);

const result = multiplyByTwo(5);
console.log(result); // Output: 10

const multiplyByTen = multiplyByTwo.bind(null, 5);

const result2 = multiplyByTen(3);
console.log(result2); // Output: 30
```

[[^]](#jsinterview)
## SOLID principals in js  

https://medium.com/backticks-tildes/the-s-o-l-i-d-principles-in-pictures-b34ce2f1e898

The SOLID principles are a set of guidelines for writing maintainable and scalable software. 

1. Single Responsibility Principle (SRP): A class or function should have only one reason to change. In JavaScript, this means that a function or object should have a single, well-defined purpose.

A class or module should have only one reason to change.
Example: Suppose you have a "User" class that handles user authentication, registration, and profile management. To apply SRP, you could split it into separate classes or modules, such as "AuthManager," "RegistrationManager," and "ProfileManager," each responsible for one of those tasks.

2. Open-Closed Principle (OCP): Software entities (classes, modules, functions, etc.) should be open for extension but closed for modification. In JavaScript, this means using composition and dependency injection instead of inheritance, and writing code that can be extended without modifying the original code.

A class or module should be open for extension but closed for modification.
Example: Suppose you have a "Product" class that calculates the total price of a product. To apply OCP, you could create an interface, such as "PricingStrategy," that defines a method for calculating the price. Then, you could create several implementations of that interface, such as "FixedPriceStrategy" and "DiscountPriceStrategy," that can be used interchangeably with the "Product" class.

3. Liskov Substitution Principle (LSP): Subtypes should be substitutable for their base types. In JavaScript, this means that objects should be designed to work with each other, and interfaces should be used to ensure that objects implement the same methods and properties.

A derived class should be substitutable for its base class.
Example: Suppose you have a "Rectangle" class that has width and height properties, and a "Square" class that inherits from "Rectangle" but always has equal width and height. To apply LSP, you could ensure that the "Square" class does not violate the behavior of the "Rectangle" class, such as by overriding the "setWidth" and "setHeight" methods to maintain the square aspect ratio.

4. Interface Segregation Principle (ISP): Clients should not be forced to depend on interfaces they do not use. In JavaScript, this means that objects should implement only the methods and properties they need, and interfaces should be designed to be small and focused.

A client should not be forced to depend on methods it does not use.
Example: Suppose you have an "Animal" interface that defines methods for walking, running, swimming, and flying. To apply ISP, you could split the interface into smaller interfaces, such as "Walkable," "Runnable," "Swimmable," and "Flyable," and have the "Animal" interface inherit from them. Then, you could implement only the interfaces that are needed by a particular animal class, such as "Bird" implementing "Flyable" and "Swimmable" but not "Runnable."

5. Dependency Inversion Principle (DIP): High-level modules should not depend on low-level modules; both should depend on abstractions. In JavaScript, this means using inversion of control and dependency injection to decouple modules and make them easier to test and maintain.

High-level modules should not depend on low-level modules; both should depend on abstractions.
Example: Suppose you have a "DataFetcher" class that retrieves data from a database and a "ReportGenerator" class that generates a report from that data. To apply DIP, you could define an interface, such as "DataRepository," that both classes depend on, and have a separate implementation of that interface, such as "DatabaseRepository," that the "DataFetcher" class uses to retrieve the data. Then, the "ReportGenerator" class can depend on the "DataRepository" interface without knowing the specific implementation used by the "DataFetcher" class.

In JavaScript, the SOLID principles can help you write clean and maintainable code. Here are some examples of how you can apply the SOLID principles in JavaScript:


------------------------------------------

[[^]](#jsinterview)
## jit & aot 
https://www.geeksforgeeks.org/what-is-aot-and-jit-compiler-in-angular/



[[^]](#jsinterview)
## providerIn in angular 

we dont need to regester the service manually in providers at globally or compnoent level,but now we don't need to regester it everywhere it'll automatically loaded where (in which compoenent it's) used, this is a great benifit when there is `n` number of service so it'll be possible sometimes that we forgot to regester in provider,

os `provierIn` provides two things `root` that's application level or you can specify to which module or components you want it should load.

previously it's happening that when we provide it in providers array it'll load with out respect its used.

This has improved loading time...by not loading all service at once only when it;s associated component or module is loaded it's instance created.

[[^]](#jsinterview)
## eager & lazy loading 

[[^]](#jsinterview)
## Change detection in angular 

When you change any of your models, Angular detects the changes and immediately updates the views. This is change detection in Angular. The purpose of this mechanism is to make sure the underlying views are always in sync with their corresponding models.

The change detection cycle is always performed once for every detected change and starts from the root change detector and goes all the way down in a sequential fashion. This sequential design choice is nice because it updates the model in a predictable way since we know component data can only come from its parent.

The change detectors provide a way to keep track of the component’s previous and current states as well as its structure in order to report changes to Angular.

There are two strategies for change detection in Angular:

* **Default change detection strategy**: In this strategy, Angular checks for changes to all components and directives in the application on every change detection cycle. This can be inefficient in large applications with many components.

* **OnPush change detection strategy**: In this strategy, Angular only checks for changes to a component or directive when its input properties have changed or an event has been triggered. This can improve performance in some cases, but requires more careful management of component state and inputs.


For OnPush :-

change detection works differently for **value types and reference types**.

For value types, such as numbers, booleans, and strings, Angular can detect changes by comparing the current value with the previous value. If the values are different, Angular will mark the component and its child components as dirty and trigger change detection. This is because value types are immutable and cannot be changed in place.

For example, consider the following component:

```
import { Component } from '@angular/core';

@Component({
  selector: 'app-my-component',
  template: '{{ myValue }}'
})
export class MyComponent {
  myValue: string = 'initial value';

  updateValue() {
    this.myValue = 'new value';
  }
}
```

In this component, we have a `myValue` property of type string. When the `updateValue()` method is called, we assign a new value to `myValue`. Because myValue is a value type, Angular can detect the change and update the view with the new value.

For reference types, such as objects and arrays, Angular cannot detect changes by comparing the current value with the previous value. This is because reference types are mutable and can be changed in place.

To detect changes for reference types, Angular uses a technique called "object identity", which compares the memory address of the object or array with the previous memory address. If the memory address is different, Angular will mark the component and its child components as dirty and trigger change detection.

For example, consider the following component:

```
import { Component } from '@angular/core';

@Component({
  selector: 'app-my-component',
  template: '{{ myArray }}'
})
export class MyComponent {
  myArray: string[] = ['initial', 'values'];

  updateArray() {
    this.myArray.push('new value');
  }
}
```
In this component, we have a myArray property of type string[]. When the updateArray() method is called, we push a new value onto the myArray array. Because myArray is a reference type, Angular cannot detect the change by comparing the current value with the previous value. Instead, Angular uses object identity to detect the change by comparing the memory address of the myArray array with the previous memory address. If the memory address is different, Angular will mark the component and its child components as dirty and trigger change detection.

It's important to note that change detection for reference types can be a performance bottleneck, especially for large objects or arrays, because Angular has to check the memory address of each reference type during each change detection cycle. To optimize performance, you can use immutable objects or implement the OnPush change detection strategy, which can reduce the number of checks performed during change detection.

[[^]](#jsinterview)
## Encapsulation  

In Angular, a component is a basic building block that encapsulates a specific part of the application's functionality. A component consists of a template, which defines the layout and structure of the component, and a TypeScript class, which contains the logic for the component.

By default, Angular components use a feature called "view encapsulation" to hide the implementation details of the component's template and styles from the rest of the application. This means that the component's styles are scoped to the component's template, and cannot be applied to other parts of the applicationy

![encapsulation](https://miro.medium.com/v2/resize:fit:828/format:webp/1*-NoQdX9CsV1jeKLg9fPsng.png)

1. None : In ViewEncapsulation.None option,
There is no Shadow DOM.
Style is not scoped to component.
<br /><br />So when we run the application, h1 style will be applied to both the components even though we have only set style in AppComponent. It happens due to NONE option.
<br /><br />
In the browser, when we examine source code, we will find that h1 style has been declared in the head section of DOM. Thus, having no Shadow DOM and also style not scoped to the component, it affects all nodes of the DOM.

2. Native ( ShadowDom ): Native keyword is removed from ng v6 In ViewEncapsulation.ShadowDOM option,
Style is scoped to the component.
Angular will create Shadow DOM for the component.
<br /><br />
Applying Shadow Dom and using AppChildComponent as child inside template of AppComponent, we can find that h1 style is applied to both components even though we have only set style in AppComponent.
<br /><br />
In the browser, when we examine source code, we will find Shadow DOM is created for AppComponent and style is also applied to its child component.

3. Emulated : is default mode in Angular where:
Angular will not create Shadow DOM for component.
Style will be scoped to the component.
<br /><br />
When we run this application, we will find h1 style from AppComponent is not applied to h1 of AppChildComponent because of emulated scoping. In this option, Angular only emulates to Shadow DOM and does not create a real Shadow DOM. Hence, styles are only scoped to the component.
<br /><br />
Examining it on the browser, Angular has created style in head section of the DOM and given an arbitrary ID to the component. On basis of ID, selector style is scoped to the component.

[[^]](#jsinterview)
## Directive & Component & Pipes 

In Angular, the Component is the one that provides data to the view. It is used to create a new View(Shadow DOM) with attached behavior. Directives in Angular are primarily used to add additional behavior to an existing DOM element or an existing component instance.

 Pipes are for formatting data, and directives are to alter the behavior/appearance of an element
