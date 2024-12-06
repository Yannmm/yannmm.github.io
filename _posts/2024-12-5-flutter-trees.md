---
layout: post
title: Widget, Element and RenderObject
tags: flutter frontend
---


- [Widget](https://api.flutter.dev/flutter/widgets/Widget-class.html) - Immutable blueprint of a part of interface.
  - Able to inflate an Element.

- [Element](https://api.flutter.dev/flutter/widgets/Element-class.html) - The use of a widget at a specific location of user interface.
  - Elements form a tree.
  - The widget associated with an element can change.

- [RenderObject](https://api.flutter.dev/flutter/rendering/RenderObject-class.html) - Handle sizing, laying out, paiting and hit-testing.
  - RenderObjects form a tree as well.
  - Deal with rendering close to the metal.