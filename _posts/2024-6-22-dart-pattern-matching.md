---
layout: post
title: Dart Pattern Matching
tags: dart flutter
---




### What

- Patterns are a `syntactic category` in the Dart language, like statements and expressions.

- A pattern may `match` a value and / or `destructure` a value.

- Patter matching check whether a given value:
    a> Has a certain shape (form).
    b> Is a certain constant.
    c> Is equal to something else.
    d> Has a certain type.

- When an object matches a pttern, the pattern can then access the object's data and extract it in parts, whcih we call `destructuring`.

- Patterns can be nested, no matter for maching patterns or destructuring patterns:
    ```
    switch (list) {
        case ['a' || 'b', var c]:
        print(c);
    }
    ```

- Patterns can appear in:
    a> Local variable declarations and assignments
    b> for and for-in loops
    c> if-case and switch-case
    d> Control flow in collection literals. This refers to `case pattern` that is `refutable`, which means either have a match or skip and continue if there is no match.


### Why

**Pattern Types**

See all the possible pattern types here: https://dart.dev/language/pattern-types. Notice, those pattern can be nested together.


**Sealed Class**

`sealed` is a class modifier, which is used to create a known, enumerable set of subtypes. This allows you to create a switch over those subtypes that is statically ensured to be "exhaustive". Because it prevents a class from being extended or implemented "outside" its own library. Sealed classes are implicitly `abstract`.


**Switch Expression**

- `switch expression` can be used wherever Dart allows expressions, except at the start of an expression statement, where a `switch statement` should be used instead.

- The syntax of a switch expression differs from switch statement syntax:
    a> Cases do not start with the case keyword.
    b> A case body is a single expression instead of a series of statements.
    c> Each case must have a body; there is no implicit fallthrough for empty cases.
    d> Case patterns are separated from their bodies using => instead of :.
    e> Cases are separated by , (and an optional trailing , is allowed).
    f> Default cases can only use _, instead of allowing both default and _.


- `switch expression / statement` can be used with `guard clause`.

### How



### Where


### When



### Who