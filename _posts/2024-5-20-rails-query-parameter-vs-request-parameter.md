---

layout: post

title: Rails: Query Parameter vs Request Parameter
tags: rails ruby

---
  

### What

[Query string](https://en.wikipedia.org/wiki/Query_string) is a part of URL that specifies parameters and values. It's most commonly used with GET request. But you can also append query string to other methods, like POST.

In Rails, these kind of parameters are called `Query Parameters`.

But for POST, data is sent within the request body. Since it's not safe at all to append your bank information in the URL.

In Rails, these kind of parameters are called `Request Parameters`. Well, they are indeed more related to request, not URL.

### Why

So what if for a POST request, when a query and a request parameter both have the same name but with different value, which will arrived at the controller action?

Good question. 

I tried myself,  found that query parameter will `override` request parameter of the same name. 
  
  
  

### How

Since Rails application is Rack-based, which means it will utilize Rack infrastructure, including parameters extraction. 

For Rack, the latter one takes precedence, which is contrary to what I tried.

So the only possibility is that the logic is overridden by Rails.

Check [here](https://stackoverflow.com/questions/8510235/rails-query-parameter-vs-post-parameter) for details.



  
  

### Where


This is a good story regarding how Rails is built upon Rack.

  

### When

  
  
  

### Who