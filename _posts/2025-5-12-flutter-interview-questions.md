---
layout: post
title: Flutter Interview Questions
tags: flutter interview
---


### Why

In past, there are a couple of times within a year I would start to learn Flutter or any other framework. I would open [roadmap.sh](https://github.com/thisissandipp/flutter-interview-questions?tab=readme-ov-file#table-of-contents) to learn it from scratch. Up unitl now I realize this is just a wast of time, since I'm only familiar with the basic concepts because I don't have the patientce to last long enough to reach the advanced toppics.

So this time, I decide to learn Flutter by preparing a real coding interview. This way, I push myself to jump right into where I'm not familiar with. Wish me good luck.

I use [Flutter Interview Questions](https://github.com/thisissandipp/flutter-interview-questions), note down my answer to the questions and expand from the question to concepts I need to refresh on and try to understand overall.

### What

1. [What is Flutter?](https://github.com/thisissandipp/flutter-interview-questions#what-is-flutter)

A: Flutter is cross-platofrm UI framework.

2. [What is Dart and Why does Flutter use it?](https://github.com/thisissandipp/flutter-interview-questions#what-is-dart-and-why-does-flutter-use-it)

A: Dart can be complied jsut in time, which is the foundation of `Hot Realod`, speeding up dev cycle. (And because Google invented Dart, this it.)

3. [What is pubspec.yaml file and what does it do?](https://github.com/thisissandipp/flutter-interview-questions#what-is-pubspecyaml-file-and-what-does-it-do)

A: `pubspec.yaml` specifies the project's dependencies.

4. [What is the difference between main() and runApp() functions in Flutter?](https://github.com/thisissandipp/flutter-interview-questions#what-is-the-difference-between-main-and-runapp-functions-in-flutter)

A: 

```
[Native OS Launches App]
          ↓
[Android: MainActivity / iOS: AppDelegate]
          ↓
[Flutter Engine Initialized]
          ↓
[Dart Runtime Starts]
          ↓
[main() Called]
          ↓
[runApp() Called → UI Built & Rendered]
```

5. [Differentiate between named parameters and positional parameters in Flutter.](https://github.com/thisissandipp/flutter-interview-questions#differentiate-between-named-parameters-and-positional-parameters-in-flutter)

A: `named paramter` is identified by key, which help with readability, while `positional paramter` idenfitied by relative position.

6. [What are widgets in Flutter?](https://github.com/thisissandipp/flutter-interview-questions?tab=readme-ov-file#what-are-widgets-in-flutter)

A: A `Widgets` describe is part of UI (Element). Widgets have not mutable state, all its fields must be final. ????