# Learn and Understand NodeJS

## 01. V8 the JavaScript Engine

### Machine Languages and C

#### Machine Languages

- Machine Languages are programming languages that are spoken by computer processors. All programs that you run on your computer has been compiled into machine code.

#### Abstraction of Programming Languages

- The following programming languages are ranked from lowest abstraction to highest abstraction:
  1. Machine Language
  1. Assembly Language
  1. C/C++
  1. JavaScript
- The important thing to know is ***Node.JS*** is written in ***C++***
- Since Node.JS is running on V8 and V8 is written in C++, this means that all JavaScript code that is running in Node.Js is actually running in a program that is written in C++.

### JavaScript Engines and the ECMAScript Specification

#### ECMAScript

- ***ECMAScript*** is the standard JavaScript is based on. It is needed since there are many engines that run JavaScript.

#### JavaScript Engine

- A ***JavaScript Engine*** is a program that converts JavaScript code into something that the computer can understand. It should follow the ECMAScript standard on how the language should work, and what features it should have.

### Adding Features to JavaScript

- We can add features to our JavaScript run-time environment by embedding the V8 engine in our application and using hooks inside it. We can write C++ code that we can then make available to applications running inside our JavaScript engine.
- An example would be that JavaScript has no support for reading files and folders. But since V8 is written in C++, we can add a file reading function to JavaScript by adding that functionality to our application that embeds V8.
- In conclusion, V8 allows us to embed it in C++ programs, and this allows us to make features inside C++ available to JavaScript. Node.JS is really just a C++ program running on the V8 engine, that has added functions that make it suitable as a server-sided language.

## 02. The Node Core

### What Does JavaScript need to Manage a Server

Below are the things that JavaScript needs to manage a server:

  1. Better ways to organize our code into reusable pieces
  1. Ways to deal with databases
  1. The ability to communicate over the Internet
  1. The ability to accept requests and send responses
  1. A way to deal with work that takes a long time

### The C Core

- The ***C++ Core*** is a core of features of utilities built in C++, made available to JavaScript, via the hooks in the V8 engine. Hence, Node.Js is not JavaScript, but is simply a C++ program that accepts JavaScript,

### The JavaScript Core

- The JavaScript core is pure JavaScript that helps make accessing the C++ functions and common JavaScript tasks and needs easier.

## 03. Modules Exports and Require

### Modules

#### Module

- A ***Module*** is a reusable block of code whose existence does not impact other code.

#### CommonJS Modules

- ***CommonJS modules*** are an agreed upon standard for how code modules should be structured.

### First-class Functions and Function Expressions

#### First-class Functions

- First-class functions are functions that are treated like objects. In other words, they can be passed around, just like objects.

#### Expressions

- An ***Expression*** is a block of code that results in a value.

#### Function Expressions

- ***Function expressions*** refer to functions that result in a value. Function expressions are possible because functions are treated like objects.

### Let's Build a Module

- Modules encapsulate code and ensures that the code inside the module doesn't affect the rest of the code in the application.
- If we want to make the code inside a module accessible to another, we use ***module.exports*** to explicitly state the object(s) that should be available to anything else that uses the module. Anything else will not be visible outside of the module.

### How do Node Modules Really Work module.exports and require

- All modules are actually wrapped in IIFEs, so that it does not pollute the global scope. This means that the variables inside the IIFE cannot be accessed outside of it.
- Example:

```JavaScript
var greet = function() {
  console.log('Hello!');
};

module.exports = greet;
```
is actually wrapped so it now becomes this:

```JavaScript
(function (exports, require, module, __filename, __dirname) {
  var greet = function() {
  console.log('Hello!');
};

module.exports = greet;
});
```

- Node then calls the function with '.apply', and then it passes in the appropriate arguments.
- The *require* method simply returns the *module.exports* of the required JavaScript file. This is because the module variable of the IIFE, is simply referring to an object and we can modify the module.exports to include stuff we wish to include inside other modules.
- In summary, ***require*** is a function that you pass a 'path' to, and it returns ***module.exports***. This works because your code is actually wrapped in a function that is given these things as function parameters.

### More on Require

- The *require* function can also be used to include a single folder, which has an index.js file inside of it.
- Inside the index.js file of your folder, you can assign module.exports to an object literal containing all the required modules inside index.js

### Module Patterns

- Node.Js caches modules that have already been required in the same file. Even if you require the module a second time, the second module reference will refer to the same object as the first module reference.
- However, if you want to have different objects across different *require*s, you can export the constructor instead of the created object. 

#### Revealing Module Pattern

- The ***Revealing Module Pattern*** exposes only the properties and methods you want via a returned object.
- This is a very common and clean way to structure and protect code within modules.

### Exports and Module.Exports

- Exports and module.exports essentially point to the same object, but with a few minor differences:
  - You can overwrite module.exports and the require statements will still work fine, but the same cannot be said for overwriting exports.
  - This is because when you overwrite *exports*, it is no longer referring to the same object as *module.exports* is, and the ***require*** keyword looks for *module.exports*, not *exports*.
  - Hence, if you want to use the *exports* keyword, you should only mutate it, not overwriting it.

### Requiring Native Core Modules

- When you require a string containing the name of a module instead of  a path, if the module is found inside the native core modules, the native module will be loaded.
- An example of a native module would be the util module, which can be imported by:

```JavaScript
const util = require('util');

util.log('hi');
```

### Modules and ES6

- ES6 modules use the export and import keywords.

```JavaScript
export function greet() {
  console.log('Hello');
}
```

```JavaScript
import * as greetr from 'greet';
greetr.greet();
```
