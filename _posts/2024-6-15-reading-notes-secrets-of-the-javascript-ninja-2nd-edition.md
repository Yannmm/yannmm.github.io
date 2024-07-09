---
layout: post
title: "Reading Notes: Secrets of the Javascript Ninjia, 2nd Edition"
tags: rails ruby
---

> Let me become a ninjia with greate Javascript skills.


### Why


TODO: check private property in closure????


### What

- JS has two pillars: a> `function`; b> `object`。

- `GUI` application's life cycle repeating two setps infinitiely: a> `Page Building`; b> `Event Handling`.

- While page building, brower will switch between parsing HTML to DOM and executing javascript code (when script node encountered) as necessary.

- HTML code is just a blueprint, DOM built from it might not be exactly the same as its original HTML.

- Browser expose global object `window`- through which all other global objects, global variables and brower APIs are accessible - to Javascript engine. 

- Browser has an environment with `single-threaded` execution model. All events, whether coming from user or server, are queued up and processed one by one.

**Functions**

Functions are `first-class` objects in Javascript. They can even posess properties:

Like, adding tag to functions:
```

var store = {
    next: 1,
    cache: {},
    add: function (fn) {
        if (!fn.id) {
            fn.id = this.next++;
            this.cache[fn.id] = fn;
            return fn.id;
        }
    }
}

function test() {}

console.log(store.add(test)); // 1
console.log(store.add(test)); // undefined

// Remember results

```

Or serve as cache:
```
function isPrime(value) {
    if (!isPrime.answers) {
        isPrime.answers = {};
    }

    if (isPrime.answers[value] !== undefined) {
        return isPrime.answers[value];
    }

    var prime = value !== 1;
    for (var i = 2; i < value; i++) {
        if (value % i === 0) {
            prime = false;
            break;
        }
    }
    return isPrime.answers[value] = prime;
}

console.log(isPrime(5)); // true
console.log(isPrime.answers[5]); // true, cached


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

**Prototyping**

`prototype` is an object to whcih the search for a particular property can be delegated to. Every object has a prototype, which also has a prototype, forming a `prototype chain`.

Every function has a [prototype](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/prototype) property. When the function is used as a constructor (instead as a "normal" function) with the `new` operator. It will become the new object's prototype.

```
function Tiger() {}
Tiger.prototype.good = 31;
const t1 = Tiger();
assert(t1 === undefined, 't1 is undefined');
const t2 = new Tiger();
assert(t2 && t2.good === 31, 't2 is a Tiger');
```

It makes sense to place `instance methods` only on the function's prototype, since in that way we have a single method shared by all instances.

Every object has a `constructor` property referencing its original constructor function, which means we can use it to instantiate more same type objects.

```
const t1 = new Tiger();
const t2 = new t1.constructor();
```


`instanceof` operator checks whether the prototype of the right-side function is in the prototype chain of the lef-side object.


To achieve object-oriented-style inheritance, we need to tamper with constructor function's prototype and monkey-patch that prototype's constructor.

```
function Animal() {}
function Tiger() {}
Tiger.prototype = new Animal();

Object.defineProperty(Tiger.prototype, "constructor", {
    enumerable: false,
    value: Tiger,
    writable: true
});

var tiger = new Tiger();
assert(tiger.constructor === Tiger, "tiger.constructor === Tiger");
assert(tiger instanceof Animal, "tiger instanceof Animal");
```

A constructor itself acts like the `class object` in ruby. The constructor constructs a new instance, who maintains a reference to the prototype. The prototype maintains a reference to the constructor as well, which is used by `instanceof` operator.

```
instance(.__proto__)
        |
        V
prototype(.constructor) ---
        |                   ^
        V                   |
Constructor(.prototype) ---
```

The ES6 keyword `class` is based on the prototype inheritance implementation.

```
class Tiger {
    constructor(name) {
        this.name = name;
        this.teeth = 30;
    }

    roar() {
        console.log('awwww');
    }

    static fight(tiger1, tiger2) {
        return tiger1.teeth - tiger2.teeth;
    }
}

class ChinaTiger extends Tiger {
    constructor(name, fur) {
        super(name);
        this.fur = fur;
    }

    smile() {
        console.log('haha');
    }
}

// Is equal to 

function Tiger(name) {
    this.name = name;
    this.teeth = 30;
}

Tiger.prototype.roar = function() {
    console.log('awwww');
}

Tiger.fight = function(tiger1, tiger2) {
        return tiger1.teeth - tiger2.teeth;
}

function ChinaTiger(name, fur) {
    this.fur = fur;
    this.constructor.prototype.name = name;
}
ChinaTiger.prototype = new Tiger();

Object.defineProperty(ChinaTiger.prototype, "constructor", {
    enumerable: false,
    value: ChinaTiger,
    writable: true
});
```

**Access Control Redefined**

Define `getter` and `setter` methods by literals:

```
const list = {
    colors: ['red', 'blue', 'green'],
    get firstColor() {
        return colors[0];
    },
    set firstColor(value) {
        colors[0] = value;
    }
}

assert(list.firstColor === 'red', 'The first color is red');

list.firstColor = 'yellow';

assert(list.firstColor === 'yellow', 'Now the first color is yellow');
```

Or using `Object.defineProperty` method:

```
function Tiger() {
    let _teeth = 12; // Create a private property using closure.

    Object.defineProperty(this, 'teeth', {
        get: () => _teeth,
        set: (value) => {
            if (value < 0) {
                throw new Error('Invalid number of teeth');
            }
            _teeth = value;
        }
    });
}

const t1 = new Tiger();
t1.teeth = 10;
assert(t1.teeth === 10, 't1.teeth === 10');

try {
    t1.teeth = -1;
    assert(false, 't1.teeth = -1 should throw an error');
} catch(e) {
    assert(e.message === 'Invalid number of teeth', 'e.message === "Invalid number of teeth"');
}
```

A `proxy` is a surrogate through which we control access to another object.

```
const emperor = { name: 'Komei' };
const representative = new Proxy(emperor, {
    get: (target, key) => {
        return key in target ? target[key] : 'The emperor is too busy to meet you now';
    },
    set: (target, key, value) => {
        target[key] = value;
    }
});

console.log(representative.name); // Komei
console.log(representative.age); // The emperor is too busy to meet you now
representative.age = 16;
console.log(representative.age); // 16

```

Handler functions, like "get" & "set", also called `traps`. Because they trap calls to the underlying target object.


### How



### Where


### When



### Who




