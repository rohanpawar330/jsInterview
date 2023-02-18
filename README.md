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
* [Promise vs Observables](#promise-vs-observables)
* [Generic Type in Typescript](#generic-type-in-typescript)
* [Interface](#interface)
* [Type vs Interface](#type-vs-interface)
* [DOM](#dom)
* [CSS Framework](#css-framework)
* [Display Flex](#display-flex)
* [Display Properties](#display-properties)
* [CSS BOX Model](#css-box-model)
* [Position Properties](#position-properties)
* [Pseudo element & pseudo class](#pseudo-element--pseudo-class)
* [Angular bootstrap](#angular-bootstrap)

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

 Pipes are for formatting data, and directives are to alter the behavior/appearance of an element.

 **Pipes**
 _here (default is `true`)_
 Are used to transform the data before it is displayed on the view. Pipes can be used to format numbers, dates, and strings, filter and sort arrays, and more.

 Custom pipe example : 

 ```
 items = [  { name: 'apple', category: 'fruit' },
    { name: 'banana', category: 'fruit' }, 
    { name: 'carrot', category: 'vegetable' },  
    { name: 'pepper', category: 'vegetable' }, 
    { name: 'orange', category: 'fruit' }];
```

```
<ul>
  <li *ngFor="let item of items | filter: 'fruit'">{{ item.name }}</li>
</ul>
```
```
import { Pipe, PipeTransform } from '@angular/core';

@Pipe({
  name: 'filter'
})
export class FilterPipe implements PipeTransform {
  transform(items: any[], filter: string): any {
    if (!items || !filter) {
      return items;
    }

    return items.filter(item => item.category === filter);
  }
}
```
the `transform` method takes an array of objects (items) and a filter value (filter) as input. The method filters the items array based on the category property and returns a new array containing only the items that match the filter criteria.

Pure Pipe :
</br>
* Pure pipes in angular are the pipes that execute when it detects a pure change in the input value.
* A pure change is when the change detection cycle detects a change to either a primitive input value (such as String, Number, Boolean, or Symbol) or object reference (such as Date, Array, Function, or Object) 

Use this by : 
```
@Pipe({
  name: 'purePipe',
  pure: true      
})
export class PurePipe {}
```

Impure Pipes:
</br>
* Impure pipes in angular are the pipes that execute when it detects an impure change in the input value. 
* An impure pipe is called on every change detection cycle in Angular. It is called on every digest cycle irrespective of the change in the input or value. If we need some pipe to be called on every change detection, mark the pipe as impure. In the case of impure pipes, Angular will call the transform() method on every change cycle
```
@Pipe({
  name: 'purePipe',
  pure: false      
})
export class PurePipe {}
```

**Directive** :
directives are used to add custom behavior to an element or to modify the behavior of an existing element. Directives can be used to manipulate the DOM, add or remove attributes, or to apply custom styling.

</br>
* Components	Used with a template. This type of directive is the most common directive type.
* Attribute directives	Change the appearance or behavior of an element, component, or another directive. `ngStyle,ngClass`
* Structural directives	Change the DOM layout by adding and removing DOM elements. `ngIf,ngFor,ngSwitch`

**ngFor** Reduce the number of calls your application makes to the server by tracking changes to an item list. With the *ngFor trackBy property, Angular can change and re-render only those items that have changed, rather than reloading the entire list of items.

```
<div *ngFor="let item of items; trackBy: trackByItems">
  ({{item.id}}) {{item.name}}
</div>
```

1. Component Directives: Component directives are used to create a custom reusable component with its own template, styles, and behavior. They are created using the @Component decorator and can be used in your templates by adding the custom element to the template. Here's an example of how to create a simple component directive:

custom directive
```
import { Directive, ElementRef } from '@angular/core';

@Directive({
  selector: '[myDirective]'
})
export class MyDirective {
  constructor(private el: ElementRef) {
    el.nativeElement.style.backgroundColor = 'yellow';
  }
}
```

[[^]](#jsinterview)
## Promise vs Observables

Both are used to handle async data...
**Promise** :  Promise works by taking a function with (optionally) two arguments resolve and reject. The passed in function executes some async code and either resolves or rejects,  Once the Promise resolves, its `.then()` method executes a handler function with the emitted value. if rejects it's get in `.catch()`.

```
let promise = new Promise((resolve) => {
  setTimeout(() => {
    resolve("some value")
  }, 1000`)
})

promise.then(value => {
  console.log(value)
})
```
</br>
**Observables** : Observables (in the JavaScript context) are the RxJS implementation of the observer design pattern. Observables are an alternative to Promises for handling async activity:

```
const { Observable } = require('rxjs');

let observable = new Observable((observer) => {
  setTimeout(() => {
    observer.next("some value")
  }, 1000)
})

observable.subscribe(value => {
  console.log(value)
})
```


*
A Promise emits a single value:
```
let promise = new Promise((resolve) => {
  resolve("a")
  resolve("b")
})

promise.then(value => console.log(value))

a
```
An Observable can emit multiple values:

```
let observable = new Observable((observer) => {
  observer.next("a")
  observer.next("b")
})

observable.subscribe(value => {
  console.log(value)
})

a
a
```
* 
Eager Loading A Promise executes the moment it is defined:
```
let promise = new Promise((resolve) => {
  console.log("promise is running")
  resolve("a")
})

console.log("start")
promise.then(value => console.log(value))
console.log("end")

promise is running
start
end
a
```

Lazy Loading An Observable executes only when subscribe() is called:

```
let observable = new Observable((observer) => {
  console.log("observable is running")
  observer.next("a")
})

console.log("start")
observable.subscribe(value => console.log(value))
console.log("end")


start
observable is running
a
end
```
*
A Promise can't be canceled. 
An Observable can be canceled via unsubscribe():
```
let observable = new Observable((observer) => {
  setTimeout(() => {
    console.log("calling next")
    observer.next("a")
  }, 1000)
})

sub = observable.subscribe(value => console.log(value))
sub.unsubscribe()
```
*
A Promise is unicast meaning you get the same value every time you call the async flow:

```
let promise = new Promise((resolve) => {
    resolve(Math.random())
})

promise.then(value => console.log(value))
promise.then(value => console.log(value))

0.768598539600432
```

An Observable is multicast meaning a separate execution occurs for every call to subscribe:

```
let observable = new Observable((observer) => {
  observer.next(Math.random())
})

observable.subscribe(value => console.log(value))
observable.subscribe(value => console.log(value))

0.6964325798899575
0.5931491554914805
```
*
The ES6 Promise doesn't have anything comparable to these operator functions...


Observables also comes with a bunch of operators which are functions that can be applied to observables. Using RxJS, you can apply functions like map() and filter() to values emitted by observables.

[[^]](#jsinterview)
## Generic Type in Typescript

 Generics allow you to create reusable components that can work with a variety of types. Generics are a way to define a type or function that can work with multiple types of data, without specifying the actual type until the code is used.
 
 </br>

In this example, the `firstElementBad` function accepts an array of `any` type and returns an `any` value. This means that it doesn't provide `any` type safety, and it's possible to pass in an array of a different type than you expect.


```
function firstElementBad(arr: any[]): any {
  return arr[0];
}

const myArray = ['hello', 'world'];
const first = firstElementBad(myArray);
console.log(first.toUpperCase()); // Error: first.toUpperCase is not a function
```

In the code above, we're passing in an array of strings, but since the firstElementBad function doesn't provide any type information, it doesn't know that the array contains strings. As a result, the first variable is assigned the value 'hello', but since first is defined as type any, TypeScript doesn't know that it's a string. When we try to call the toUpperCase method on first, TypeScript raises a runtime error, because it doesn't know that first is a string and doesn't have a toUpperCase method.


This kind of error can be hard to catch at compile time, and can lead to unexpected behavior and runtime errors in your code. By using generics and providing more specific type information, you can avoid these kinds of errors and make your code more type safe


```
function firstElement<T>(arr: T[]): T {
  return arr[0];
}


const myArray = ['Hello', 'hi', 'how'];
const first = firstElement<number>(myArray); // returns 'Hello'
```

TypeScript can ensure that you're getting the correct type of value back, and you can use the firstElement function with any type of array.

[[^]](#jsinterview)
## Interface

an interface is a way to define a contract for an object, specifying the properties and methods that the object must have. It is a type that defines the shape of an object, but does not provide an implementation.

An interface can be thought of as a set of rules or requirements that an object must follow in order to be considered a valid implementation of the interface. For example, if you have an interface called User that defines a property called name, any object that implements the User interface must have a property called name of a specific type.

```
interface User {
  name: string;
  age: number;
  email?: string;
  sayHello(): void;
}
```
[[^]](#jsinterview)
## Type vs Interface

 Both type and interface can be used to define custom types, but they have some differences in terms of their syntax and intended use.

 * syntax

 ```
 type Age = number;

 interface Person {
  name: string;
  age: number;
}
```
* use

Interfaces are primarily used to define contracts for objects, specifying the properties and methods that an object must have. Interfaces can also be extended and merged together to create more complex interfaces.

Types, on the other hand, are used to create aliases for other types. This is useful when you want to create a shorter, more readable name for a complex type or a union of types.

* Extensibility

Interfaces can be extended to create more specific interfaces that inherit properties from the base interface.

```
interface Person {
  name: string;
}

interface Employee extends Person {
  salary: number;
}
```
Types cannot be extended in the same way, but they can be combined using the | operator to create union types:

```
type Age = number;
type Name = string;
type AgeOrName = Age | Name;
```
[[^]](#jsinterview)
## DOM

The DOM is a tree-like structure, where each element of an HTML document is represented by a node in the tree. The root of the tree is the document object, which represents the entire HTML document. Other nodes in the tree represent HTML elements, such as `<html>, <head>, <body>, and <div>,` as well as text nodes, attribute nodes, and other types of nodes.

HTML is used to structure the web pages and Javascript is used to add behavior to our web pages. When an HTML file is loaded into the browser, the javascript can not understand the HTML document directly. So, a corresponding document is created(DOM). DOM is basically the representation of the same HTML document but in a different format with the use of objects. Javascript interprets DOM easily i.e javascript can not understand the `tags(<h1>H</h1>)` in HTML document but can understand object h1 in DOM. Now, Javascript can access each of the objects (h1, p, etc) by using different functions.

![DOM](https://media.geeksforgeeks.org/wp-content/uploads/DOM.png)

[[^]](#jsinterview)

## CSS Framework

A CSS framework is a pre-written collection of CSS files, which contain a set of rules and guidelines for styling HTML elements. It's a standardized approach to web development that makes it easier and faster to create consistent, responsive and mobile-friendly web designs.

[[^]](#jsinterview)
## Display Flex

The Flexible Box Module, usually referred to as flexbox, as a method that could offer space distribution between items in an interface and powerful alignment capabilities.

The main axis is defined by `flex-direction`, which has four possible values:

* row
* row-reverse
* column
* column-reverse

[[^]](#jsinterview)

## Display Properties

The `display` property specifies the display behavior (the type of rendering box) of an element.

```p.ex1 {display: none;}
p.ex2 {display: inline;}
p.ex3 {display: block;}
p.ex4 {display: inline-block;}
```

**none**	The element is completely removed

**inline**	Displays an element as an inline element `(like <span>)`. Any height and width properties will have no effect

**block	Displays** an element as a block element `(like <p>)`. It starts on a new line, and takes up the whole width

**inline-block**	Displays an element as an inline-level block container. The element itself is formatted as an inline element, but you can apply height and width values

[[^]](#jsinterview)

## CSS BOX Model

![CSS Box Model](https://www.freecodecamp.org/news/content/images/2021/08/Screenshot-2021-08-29-at-3.13.33-PM.png)

[[^]](#jsinterview)

## Position Properties

The `position` property specifies the type of positioning method used for an element `(static, relative, absolute, fixed, or sticky).`

**Static**	Default value. Elements render in order, as they appear in the document flow,The element is positioned according to the normal flow of the document. The top, right, bottom, left, and z-index properties have no effect. This is the default value.

**position: relative** works the same way as position: static;, but it lets you change an element's position.

But just writing this CSS rule alone will not change anything.

To modify the position, you'll need to apply the` top, bottom, right, and left` properties mentioned earlier and in that way specify where and how much you want to move the element.

**Absolute** The element is removed from the normal document flow, and no space is created for the element in the page layout. It is positioned relative to its closest positioned ancestor, if any; otherwise, it is placed relative to the initial containing block. Its final position is determined by the values of top, right, bottom, and left.

**The fixed** positioning property helps to put the text fixed on the browser. This fixed test is positioned relative to the browser window, and doesn't move even you scroll the window.

**Sticky** It's treated as relatively positioned until its containing block crosses a specified threshold (such as setting top to value other than auto) within its flow root (or the container it scrolls within), at which point it is treated as "stuck" until meeting the opposite edge of its containing block.

**z-index**	It is used to set stack order of an element.

[[^]](#jsinterview)

## Pseudo element & pseudo class

**Pseudo element** : A CSS pseudo-element is used to style specified parts of an element.

For example, it can be used to:

Style the first letter, or line, of an element
Insert content before, or after, the content of an element
```
selector::pseudo-element {
  property: value;
}

p::first-letter {
  color: #ff0000;
  font-size: xx-large;
}
```

>The double colon replaced the single-colon notation for pseudo-elements in CSS3. This was an attempt from W3C to distinguish between pseudo-classes and pseudo-elements.

**A pseudo-class** is used to define a special state of an element.

For example, it can be used to:

Style an element when a user mouses over it
Style visited and unvisited links differently
Style an element when it gets focus

```
selector:pseudo-class {
  property: value;
}

/* unvisited link */
a:link {
  color: #FF0000;
}

/* visited link */
a:visited {
  color: #00FF00;
}

/* mouse over link */
a:hover {
  color: #FF00FF;
}

/* selected link */
a:active {
  color: #0000FF;
}

```
:first-child	p:first-child	Selects every `<p>` elements that is the first child of its parent

:nth-child(n)	p:nth-child(2)	Selects every `<p>` element that is the second child of its parent

:nth-last-child(n)	p:nth-last-child(2)	Selects every `<p>` element that is the second child of its parent, counting from the last child

[[^]](#jsinterview)

## Angular bootstrap

1. ANGULAR.JSON File </br>
ANGULAR.JSON is the file which has various properties and configuration of your Angular project. This is the file which is first referred by the builder to look for all the paths and configurations and to check which is the main file.

```
"options":{  
    "outputPath":"dist/hello-world",
    "index":"src/index.html",
    "main":"src/main.ts",  // THIS LINE
    "polyfills":"src/polyfills.ts",
    "tsConfig":"src/tsconfig.app.json",
    "assets":[  
       "src/favicon.ico",
       "src/assets"
     ],
    "styles":[  
       "node_modules/bootstrap/dist/css/bootstrap.min.css",
       "src/styles.css"
     ],
    "scripts":[],
    "es5BrowserSupport":true
}
```

2. MAIN.TS </br>
This file acts as the entry point of the application. After this, main.ts file calls the function bootstrapModule(AppModule) which tells the builder to bootstrap the app.

```
platformBrowserDynamic().bootstrapModule(AppModule)
```

3. APP.MODULE.TS </br>
This is the module, created with the @NgModule decorator, which has declarations of all the components we are creating within the app module so that angular is aware of them. Here, we also have imports array where we can import other modules and use in our app.

```
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { FormsModule } from '@angular/forms';
import { AppComponent } from './app.component';
import { TestComponent } from './test/test.component';
@NgModule({
   declarations: [
      AppComponent,
      TestComponent
   ],
   imports: [
      BrowserModule,
      FormsModule
   ],
   providers: [],
   bootstrap: [AppComponent]
})
export class AppModule { }
```
4. APP.COMPONENT.TS </br>
This is the file which interacts with the html of the webpage and serves it with the data. The component is made by using @Component decorator which is imported from @angular/core. The component has a selector, which is like a custom html tag which we can use to call that component. It then has template or templateUrl which contains the html of the page to be displayed. It also has the styleUrls array where component specific style sheets can be placed.

```
import { Component } from '@angular/core';
@Component({
   selector: 'app-root',
   templateUrl: './app.component.html',
   styleUrls: ['./app.component.css']
})
export class AppComponent {
   title = 'hello-world';
}
```

5. INDEX.HTML </br>
Now, since angular is well aware of the modules, components, styles, scripts etc. which are required to display the page.</br>
 the index.html file is called. It is found in the src folder of the app. Compiler dynamically adds all the javascript files at the end of this file. Since all the components are now known, the html file calls the root component that is app-root. 
 ```
 <!doctype html>
 <html lang="en">
    <head>
       <meta charset="utf-8">
       <title>My Hello World App!</title>
       <base href="/">
       <meta name="viewport" content="width=device-width, initial-scale=1">
       <link rel="icon" type="image/x-icon" href="favicon.ico">
    </head>
    <body>
       <app-root></app-root>
    </body>
 </html>
 ```

 6. APP.COMPONENT.HTML </br>
This is the file which contains all the html elements and their binding which are to be displayed when the app loads. Contents of this file are the first things to be displayed.
