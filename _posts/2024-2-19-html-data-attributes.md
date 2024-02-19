---
layout: post
title: HTML Data Attributes
tags: web html
---

## Why

The [data-* attributes](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/data-*) allows us to store extra information on HTML elements without having to use a non-semantic element or pollute the class name. They can contain information that is constantly changing, like a score in a game. It's not a good idea to put content that is visible and accessible.

  

**Reference**: [Using data-* attributes in JavaScript and CSS - Mozilla Hacks - the Web developer blog](https://hacks.mozilla.org/2012/10/using-data-attributes-in-javascript-and-css/)

  

## What

`data-*` custom attributes are [global attributes](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes). `*` may be replaced by any lowercased alphabet characters (except `xml`) and `-`. The attribute value must be type of `String`.

  

## How

Developers can access an element's custom data attributes via:

For **Javascript**, access them through [HTMLElement](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement)' [dataset](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/dataset) properties, which is a [DOMStringMap](https://developer.mozilla.org/en-US/docs/Web/API/DOMStringMap) with an entry for each `data-*` attribute. Get a custom data attribute, [convert](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/dataset#name_conversion) the part of the attribute name after `data-`.


**CSS**
Use [attr()](https://developer.mozilla.org/en-US/docs/Web/CSS/attr) function to retrieve the attribute value. Or use [attribute selectors](https://developer.mozilla.org/en-US/docs/Web/CSS/Attribute_selectors) to changes styles according to the value.
  

## Where

Add custom data attributes to `HTML` elements directly.

  

## When

Before accessing custom data attributes, you need to retrieve the element first.

  

## Who