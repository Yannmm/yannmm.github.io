---
layout: post
title: Absolute Path, Relative Path And Root Relative Path
tags: web javascript
---

### What
 In web-development, linking to another page, external stylesheet, javascript file, images are common practices. There are three ways to declare the file path.

### How

- **Absolute Path** - put the entire URL to the file. The avantage is easy to deal with. And this is the only way to link to files on another domain.

	```
	<img  src="http://www.webdevbydoing.com/wp-content/uploads/beach.jpg">
	```

	To ensure current page's protocol is respected, prefix the path with `//`.

	```
	<img  src="//www.webdevbydoing.com/wp-content/uploads/beach.jpg">
	```

- **Relative Path** - the path is relative to the current path. This provides advantage of transferrable code, like if the domain changes.

	```
	// bean.jpg is in the same directory as current file
	<img  src="beach.jpg">

	// bean.jpg is in images directory which is in the same directory as current file
	<img  src="images/beach.jpg">

	// bean.jpg is in the parent directory
	<img  src="../beach.jpg">
	```
  
- **Root Relative Path** - always try to find the file relative to the root of the website by prefixing the path with `/`. It kind of enjoys advantages from above two.

	```
	<img  src="/wp-content/uploads/beach.jpg">
	```


### Why

Maybe this is tradition which originating in Unix file system, since it has some conventions to represent directory shortcut.
  
 
  

### Where

In `.html` and `.js` files.
  
  

### When


  
  

### Who


### Refs

- [Absolute File Paths VS. Relative File Paths VS. Root Relative Paths - WebDevBydoing](https://www.webdevbydoing.com/absolute-relative-and-root-relative-file-paths/)