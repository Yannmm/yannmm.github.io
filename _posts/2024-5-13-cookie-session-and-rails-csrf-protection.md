---

layout: post

title: Cookie, Session & Rails CSRF Protection

tags: rails ruby

---
    

### What

**Cookies**

A cookie is a small piece of data a server sends to a user's web browser. The browser stores cookies and send them back to the sever in later requests. It's the only way to store limited amounts of data, remembering state information. Since by default HTTP protocol is `stateless`.

The server is able to set cookies using `Set-Cookie` header and read cookies using `Cookie` header, in response and request respectively.

This [article](https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies) explains details.


**Session**

A session can refer to one of two things:

1. A place to store data during one request that can be used in later requests.
2. A time period during which the user is logged in to your application.

Generally, once a user logs in, the application stores his information in the session (the place). And use that information in subsequent request to make sure the user is valid and logged-in (the period).

For rails, several store mechanisms are provided, you can store session data in any of them via a `unified` API.

-  `CookieStore`: Store all data inside a cookie, in addition to the session ID
-  `CacheStore`: Store data inside the Rails cache
-  `ActiveRecordStore`: Store the data in the database
-  `MemCacheStore`: Use a Memcached cluster of servers

A session id is generated when the session data is stored. It' set in the `cookie`, no matter whichever store you use.


This [article](https://www.writesoftwarewell.com/rails-sessions/#how-do-sessions-work) has great explanation.




### Why

The key difference between sessions and cookies is that **sessions are saved on the server side while cookies are saved on the client side**.
  

### How

**CSRF & CSRF Protection**

Cross-site request forgery is a malicious exploit of a website that unauthorized commands are transmitted from a user the website trusts. The attacker usually induces users to performa actions they do not intend to by a fake `form`, which triggers state change request, e.g, transfer money from users' account to the attacker's. 

 

### Where


Rails insert `CSRF-token` into both `form` and `meta` tag. 

The former one will be sent along in the payload when form is submitted. 

The latter one is to give javascript requests that are not tied to a form an easy way of getting the token. If you use the [jquery-ujs](https://github.com/rails/jquery-ujs) library the content of that meta tag is automatically added (as a request header) to any ajax requests made (in the `X-Csrf-Token` request header?).

Token is generated on the fly for each request. During generation, it's inserted into session, making sure the one embedded in html alway matches the one in the session.
 
### When

Since a request can pass in the `CSRF-token` through form params or `X-Csrf-Token` header, Rails requires at least one of those tokens match the one in the session.

```
# Possible authenticity tokens sent in the request.
def request_authenticity_tokens 
	[form_authenticity_param, request.x_csrf_token]
end
```

Check this [article](https://medium.com/rubyinside/a-deep-dive-into-csrf-protection-in-rails-19fa0a42c0ef) for detailed explanation.

### Who



**References**
- [A Deep Dive into CSRF Protection in Rails | by Alex Taylor | Ruby Inside | Medium](https://medium.com/rubyinside/a-deep-dive-into-csrf-protection-in-rails-19fa0a42c0ef)
- [Using HTTP cookies - HTTP | MDN (mozilla.org)](https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies)
- https://stackoverflow.com/a/359482/10616866
- [What Are Sessions? How Do They Work? | Baeldung on Computer Science](https://www.baeldung.com/cs/web-sessions)
- [Sessions in Rails: Everything You Need to Know (writesoftwarewell.com)](https://www.writesoftwarewell.com/rails-sessions/#how-do-sessions-work)