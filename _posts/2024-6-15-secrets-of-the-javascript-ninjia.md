---
layout: post
title: "Reading Notes: Secrets of the Javascript Ninjia, 2nd Edition"
tags: rails ruby
---

> Let me become a ninjia with greate Javascript skills.


### Why




### What

- JS has two pillars: a> `function`; b> `object`。

- `GUI` application's life cycle repeating two setps infinitiely: a> `Page Building`; b> `Event Handling`.

- While page building, brower will switch between parsing HTML to DOM and executing javascript code (when script node encountered) as necessary.

- HTML code is just a blueprint, DOM built from it might not be exactly the same as its original HTML.

- Browser expose global object `window`- through which all other global objects, global variables and brower APIs are accessible - to Javascript engine. 

- Browser has an environment with `single-threaded` execution model. All events, whether coming from user or server, are queued up and processed one by one.

- Functions are `first-class` objects in Javascript.

- Javascript Functins can even posess properties:
    ```
        var f = funciton() {};
        f.name = "Hanzo";
    ```

- 4 ways to define functions in Javascript:
    a> Function declarations
    b> Function expressions
    c> Arrow functions
    d> Function constructors (obsolete)
    e> Generator functions

- To immediately call to a function expression, using parentheses to signal to parser this is an expression, not a declaration:
    ```
    (function() {})(3);
    ```

- `arguments` and `this` are two implicit function parameters.

- `this` is affected by the way to invoke the function, when invoked:
    a> As a function, `this` is either `window` (nonstrict mode) or `undefined` (strict mode):
        ```
            function f1() => this; 
            function f2() { 'use strict'; return this; }
            
            f1(); // Window
            f2(); // undefined
        ```
    b> As a method, `this` refers to owner of the function property:
        ```
            function f1() => this;

            f1(); // window

            let k1 = {
                func: f1
            };
            k1.func(); // k1

            let k2 = {
                func: f1
            };
            k2.func(); // k2
        ```
    c> As a constructor: `new F1()`
    d> Via the function's apply or call methods: `f1.call() / f1.apply()`

### How



### Where


### When



### Who