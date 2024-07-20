---
layout: post
title: Rails Cookies Guide
tags: rails ruby
---




### What are Cookies?

Since HTTP protocol is `stateless`, to maintain state among subsequent requests, web applications need a mechanism to store and exachenge information with the server.

When the user visits a website, the server will send a small piece of data long with the response. This small piece of data is called a cookie. When the browser receives the response, it will save any cookies coming along into its internal storage. Most importantly, the browser sends those cookies to the same server for each subsequent request.

As an information exchange mechanism, Cookies is not limited to `Session Management`. It can also be used by `Personalization` and `Tracking`.

![Cookie Cycle](https://ibb.co/7QC0pbT)

### Cookie Usage 

The server is able to set one ore more cookies via `Set-Cookie` response header. Each `Set-Cookie` stands for a key-value pair.

```
HTTP/2.0 200 OK
Content-Type: text/html
Set-Cookie: username=akshay
Set-Cookie: theme=railscasts

[page content]
```

The browser will send back previously received cookies back to the server in the `Cookie` request header.

```
GET /sample_page.html HTTP/2.0
Host: www.rubyonrails.org
Cookie: username=akshay; theme=railscasts
```

### Accessing Cookies in Rails

Rails provides [cookies](https://api.rubyonrails.org/classes/ActionController/Cookies.html#method-i-cookies) to contorllers, views and helpers. It's hash-like object.

```
class CommentsController < ApplicationController
  def new
    @comment = Comment.new(author: cookies[:commenter_name])
  end

  def create
    cookies[:commenter_name] = @comment.author
    
    # or
    
    cookies.delete(:commenter_name)
  end
end
```

### Lieftime of a Cookie

Each cookie has a lifetime after which it expires. By default, the browser drops the cookies after you quit. Use `Expire` attribute to tell the browser when to delete the cookie, or `Max-Age` to specify a period of time of storage.

```
Set-Cookie: font=monaco; Expires=Thu, 31 Oct 2021 07:28:00 GMT;
```

In Rails, use `expires` key. It takes a number of seconds, a timestamp or a ActiveSupport::Duration object.

```
# Sets a cookie that expires in 1 hour.
cookies[:theme] = { value: "monokai", expires: 20.minutes.from_now }

# Sets a cookie that expires on the specified time.
cookies[:theme] = { value: "railscasts", expires: Time.utc(2023, 4, 5) }
```

You can also set `permanent` cookies that never expire.

```
# Sets a "permanent" cookie (which expires in 20 years from now).
cookies.permanent[:plan] = "basic"
```

### Restrict Cookie Access

Certainly cookies cannot be sent to any website as the browser likes to. It use the cookie scope to determine this. The scope consistes of `Domain`, `Path` and `SameSite`.

The `Secure` attribute ensure that the cookie are only sent to the server via `HTTPS` protocol.

The `HttpOnly` attribute prevents the client-side javascript code to read the cookie via `Document.cookie` API.


```
Set-Cookie: id=ak_98; Expires=Fri, 22 Oct 2021 07:28:00 GMT; Secure; HttpOnly
```

Rails provides corresponding options:

```
cookies[:account_number] = { value: @account.number, secure: true, httponly: true }
```

### Sign and Encrpyt Cookies

Since cookies are stored at client-side, of course they can be read and changed. Next time the browser send a request, modified cookies will be sent along.

To allow the user to read the cookie but not modify it, Rails can sign the cookie:

```
# create a signed cookie
cookies.signed[:user_id] = current_user.id

# read a signed cookie
cookies.signed[:user_id]
```

Rails will appends a cryptographic signature to the cookie value. Once modified, it will be discarded.

To prevent the user from both reading and modifying the cookie, Rails can encrypt it:

```
# write an encrypted cookie
cookies.encrypted[:user_id] = current_user.id

# read an encrypted cookie
cookies.encrypted[:user_id]
```

This is achieved by Rails not only sign the cookie but also encrypt it.



### References

- [The Complete Guide to Working With Cookies in Rails](https://www.writesoftwarewell.com/how-http-cookies-work-rails/)

