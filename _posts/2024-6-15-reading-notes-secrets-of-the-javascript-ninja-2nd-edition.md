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
    c> As a constructor, calling a function with keyword `new` will create a new empty object referenced by `this` and return the newly constructed object as the `new` operator's return value. (Explicit return value will be ignored if it's non-object.)
        ```
        function Ninja() {
            this.shout = () => this;
        }
        let n1 = new Ninja();
        ```

    d> Via the function's apply or call methods, we can set `this` explicitly.
    e> `arrow` functions inherit context from where it's defined.
    f> `bind` method create a brand-new function with `this` set explicitly.








**Generators**

`Generators` are able to produce multiple values, on a per request basis, suspending their execution between these requests. 

One merit is that its cntext is reserved and resumed between each execution. This creates an isolated environment.

Another merit is allowing treat asynchronous code in synchronous way, since it emits one value at a time. This means a generator must be one of following states: a> idle; b> executing; c> suspended; d> completed.

Notice, `return` only ends the geneartor (in complete state), the value after return is not yielded.

One way to consume a sequence of generated values is using `for-of` loop:

```
function* g1() {
    yield 'a'
    yield 'b'
    yield 'c'
}

for(let weapon of g1()) {
    console.log(weapon)
}
```

Making a call to a generator does not mean the body of generator function will be executed immediately. Instead, an iterator object is created.

```
function* g1() {
    yield 'a'
    yield 'b'
    yield 'c'
}

const iterator = g2();

iterator.next(); // a
iterator.next(); // b
iterator.next(); // c
iterator.next(); // undefined

```

`next` and `yield` are zipped together and next always comes first. And, starting from the second next, you can provide arugment so it will serve as the return value of previous `yield`.

```
function* g3(name) {
    const r1 = yield('good' + ' ' + name);
    yield('bad' + ' ' + r1);
}

const iterator = g3('John');

iterator.next('A'); // good John

iterator.next('B'); // bad B
```


By using `yield*`, we yield (transfer control) to another generator.

```
function* g1() {
    yield 'a';
    yield 'b';
    yield* g2();
    yield 'c';
}

function* g2() {
    yield 1;
    yield 2;
    yield 3;
}
```

`throw` is used to pass error from inside and outside of a generator.

```
function *g4() {
    try {
        yield 123;
        throw 'from inside'
    } catch(e) {
        cnsoel.log(e);
    }
}

const iterator = g4();
iterator.throw('from outside');
```

**Promises**

A `Promise` is an placeholder for the result of an asynchronous task. It's either in **pending** or **resolved** state. 

```
const p1 = Promise((resolve, reject) => {
    resolve('Good');
    // Or
    // reject('An error happened');
});

p1.then(result => { console.log('this is good.') }, err => { console.log('something bad happend') });
```

`catch()` method will catch any error produced in a chain of promises.


`async` keyboard actually converts a function into a geneartor; while `await` mark wating for a promise to complete. 


```
// Raw implementation of async & await
function async(generator) {
    var iterator = generator();

    function handle(result) {
        if (result.done) { return; }
        const value = result.value;

        if (value instanceof Promise) {
            value.then(r => handle(iterator.next(r))).catch(e => iterator.throw(e));
        }
    }

    try {
        handle(iterator.next());
    } catch(e) {
        iterator.throw(e);
    }
}

// Usage
async(function* () {
    try {
        const task1 = yield getTask1();
        const task2 = yield getTask2();
        const task3 = yield getTask3();
    } catch(e) {
        console.log(e);
    }
});

// Using async and await keywords
async function () {
    try {
        const task1 = yield getTask1();
        const task2 = yield getTask2();
        const task3 = yield getTask3();
    } catch(e) {
        console.log(e);
    }
}()
```

### How



### Where


### When



### Who




