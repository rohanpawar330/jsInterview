# jsInterview

## js work


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

## Javascript is single-threaded

_JavaScript_ is called a ***"single-threaded"*** language because it can only execute one piece of code at a time. This means that if one function is running, it has to finish before another function can start.

JavaScript has a single `call stack`, which is a data structure used by the JavaScript engine to keep track of which functions are currently running and in what order. 

JavaScript code must be written in a way that avoids long-running or blocking operations, as these can cause the user interface to freeze and become unresponsive.

JavaScript is single-threaded, it can still make use of asynchronous operations like _callbacks, promises, and async/await_ to handle multiple tasks without blocking the main thread. Additionally, modern web browsers have introduced Web Workers, which allow JavaScript code to run in separate threads for heavy computation, but these are still relatively limited in use.

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

## SOLID principals in js

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

## jit & aot
https://www.geeksforgeeks.org/what-is-aot-and-jit-compiler-in-angular/



## providerIn in angular

we dont need to regester the service manually in providers at globally or compnoent level,but now we don't need to regester it everywhere it'll automatically loaded where (in which compoenent it's) used, this is a great benifit when there is `n` number of service so it'll be possible sometimes that we forgot to regester in provider,

os `provierIn` provides two things `root` that's application level or you can specify to which module or components you want it should load.

previously it's happening that when we provide it in providers array it'll load with out respect its used.

This has improved loading time...by not loading all service at once only when it;s associated component or module is loaded it's instance created.

## eager & lazy loading

## Change detection in angular

There are two strategies for change detection in Angular:

* **Default change detection strategy**: In this strategy, Angular checks for changes to all components and directives in the application on every change detection cycle. This can be inefficient in large applications with many components.

* **OnPush change detection strategy**: In this strategy, Angular only checks for changes to a component or directive when its input properties have changed or an event has been triggered. This can improve performance in some cases, but requires more careful management of component state and inputs.

