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

  

  

### How

- `Turbo Stream` does not work with `GET` method. Not sure why, but with browser inspector, we can see that turbo has taken over all http calls. (Click any link or button then go to browser inspector -> network -> select a request -> check the `initiator` panel. Some `turbo.es2017-esm.js` javascript framework make the actual http call). Turbo adds `text/vnd.turbo-stream.html` to `Accept` of request header, along with other default content-type (text/html, application/xhtml+xml) for `non-Get` requests. For `Get` requests, `Accept` is not modified. 

 - Seems the content-type in `Accept` of request header is served by order. ie, for `text/vnd.turbo-stream.html, text/html, application/xhtml+xml`, `text/vnd.turbo-stream.html` is served as response from format collector of `respond_to` block. Maybe this is another rails convention.

- `Turbo stream` allows you to send more than one actions (against different targets) in one response. From backend you can do it in the `render turbo_stream` method or put them in the `?.turbo_stream.erb` template. Quite flexible.
  

### Where

  

  

### When

  

  

### Who

  
  

### References:

  

- [Turbo Handbook: Frames](https://turbo.hotwired.dev/handbook/frames)

- [Turbo Reference: Attributes](https://turbo.hotwired.dev/reference/attributes)

