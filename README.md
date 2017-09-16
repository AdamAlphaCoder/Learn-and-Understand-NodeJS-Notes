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

- The V8 engine not only can convert JavaScript code into Machine code, but also can convert JavaScript code into C++ code, since the V8 engine is written in C++.
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
