---

  

  

  

layout: post

  

  

  

title: Hotwire - Turbo Frame

  

  

  

tags: rails ruby turbo hotwire

  

  

  

---

  

  

  

### Why

  

  

  

`Turbo Drive` is a drop-in replacement that enables speeding up navigation.

  

  

  

`Turbo Frame` allows predefined parts of a page to be updated on request. Any links and forms inside a frame are captured, and the frame contents automatically updated after receiving a response.

  

  

  

Frames are created by wrapping a segment of the page in a `<turbo-frame>` element. Each element must have a unique ID, which is used to match the content being replaced when requesting new pages from the server. A single page can have multiple frames, each establishing their own context.

  

  

  

In most cases, requests that originate from a `<turbo-frame>` are expected to fetch content for that frame (or for another part of the page, depending on the use of the `target` or `data-turbo-frame` attributes). This means the response should always contain the expected `<turbo-frame>` element. If a response is missing the `<turbo-frame>` element that Turbo expects, it’s considered an error; when it happens Turbo will write an informational message into the frame, and throw an exception.

  

  

  

  

### What

  

  

### When

  

A major contributor of the turbo framework said that developers should always try `frame` first, then seek `stream` if the former one does not resolve the problem. I think one of good thing for `Turbo Frame` is that it require little the code amount for a new codebase and little effort for an existing one.

  

  

### How

  

**Turbo Frame**

  

- By default `Turbo Frame` is [eager-loading](https://turbo.hotwired.dev/reference/frames#eager-loaded-frame). But it can be [lazy-loading](https://turbo.hotwired.dev/reference/frames#lazy-loaded-frame) by setting attribute `loading: "lazy"`. This means it won't loading from `src` until the frame element is visible. But be noticed, the frame element will never load if you put it at the end of page since it's never visible.

  

- It blows my mind how to use `lazy-loading` frame to accomplish `scroll-to-bottom-to-load-more` effect. No javascript at all! One caveat is that you need to embed the `next-page frame` into `current-page frame`. So in the end you'll find many nested frames. [(70) Ruby on Rails #68 Frames: Infinite Scroll Pagination - YouTube](https://www.youtube.com/watch?v=OEuNR3XGvPk&t=452s)

  

**Turbo Stream**

 - I just wonder the `template.turbo_stream.erb` stuff only works for `stream`, or it works for `frame` as well. It seems the client-side turbo javascript framework only adds `text/vnd.turbo-stream.html` to `ACCEPT` headers for a non-GET request.

- Another cool technique is we usually `REDIRECT` for a `DO` request (eg: `POST/PUT/PATH`) while `SHOW` something for `GET` request. Those are common patterns. But with `turbo_stream`, we can perform `DO-SHOW` rather than `DO-REDIRECT`. This is done by create a corresponding template in views, like if you want to update the view item when you update a record, just create file `create.turbo_stream.html.erb` in the views folder, specifying `turbo_stream` action there. No need to explicitly `respond_to`, rails will automatically find that template and render.

-  `Turbo Stream` does not work with `GET` method. Not sure why, but with browser inspector, we can see that turbo has taken over all http calls. (Click any link or button then go to browser inspector -> network -> select a request -> check the `initiator` panel. Some `turbo.es2017-esm.js` javascript framework make the actual http call). Turbo adds `text/vnd.turbo-stream.html` to `Accept` of request header, along with other default content-type (text/html, application/xhtml+xml) for `non-Get` requests. For `Get` requests, `Accept` is not modified.

  

  

- Seems the content-type in `Accept` of request header is served by order. ie, for `text/vnd.turbo-stream.html, text/html, application/xhtml+xml`, `text/vnd.turbo-stream.html` is served as response from format collector of `respond_to` block. Maybe this is another rails convention.

  

  

-  `Turbo stream` allows you to send more than one actions (against different targets) in one response. From backend you can do it in the `render turbo_stream` method or put them in the `?.turbo_stream.erb` template. Quite flexible.

  

  

### Where

  

  

  

  
  
  

  

  

  

### Who

  

  

  

### References:

  

  

  

- [Turbo Handbook: Frames](https://turbo.hotwired.dev/handbook/frames)

  

  

- [Turbo Reference: Attributes](https://turbo.hotwired.dev/reference/attributes)