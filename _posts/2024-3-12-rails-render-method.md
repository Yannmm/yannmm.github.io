---

  

layout: post

  

title: Rails render & respond_to Method

  

tags: rails ruby

  

---

  

  

### Why

  

  

  

### What

  

  

Both `ActionView` and `ActionController` has `render` method.

  

  

- [render]((https://api.rubyonrails.org/classes/ActionController/Rendering.html#method-i-render))

  

- [render]((https://api.rubyonrails.org/classes/ActionView/Helpers/RenderingHelper.html#method-i-render)) this one has `render formats: [:json, :html]`, as search `:formats` in the [source code](https://github.com/rails/rails/blob/main/actionview/lib/action_view/lookup_context.rb#L18)

  

  

It's confusing the [documentation](https://guides.rubyonrails.org/layouts_and_rendering.html) mix those two methods together.

  

  

  

### How

  

The controller is able to `render` explicitly or implicitly.

  

- Implicit: If you do not explicitly render something at the end of a controller action, Rails will automatically look for the `action_name.html.erb` template in the controller's view path and render it.

- Explicit:

-  `render` to render whatever stuff in named format. The content may be current action's template, some other action's template in or not in the same controller, a file, a raw string, etc.

-  `respond_to` to describe what to return for different requested formats.

  

  

  

### Where

  

  

  

### When

  

`respond_to` might play a supplemental role for `render`. As the doc states: `render` renders a template and assigns the result to `self.response_body`. And since the very beginning, only two formats are supported natively: `html` & `json`. While `respoind_to` act as a DSL, allowing us to describe what to respond for different formats requested. The doc for `respond_to` constantly mentions `web-service`, which it means certain rack-compliant web server that brings requested format information to our rails controller. So within `respond_to`, we can define what to return with the `format` object.

  
  

references: [What's the difference between using render instead of respond_with/to in a Rails API? - Stack Overflow](https://stackoverflow.com/questions/31378177/whats-the-difference-between-using-render-instead-of-respond-with-to-in-a-rails)

  

### Who

It's very interesting to read [ActionController::Base](https://api.rubyonrails.org/v7.1.3.2/classes/ActionController/Base.html) and [ActionView::Base](https://api.rubyonrails.org/v7.1.3.2/classes/ActionView/Base.html). Those two `Base` classes play vital roles in dealing with web request.