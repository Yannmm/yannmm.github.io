---
layout: post
title: Rails Render Method
tags: rails ruby
---

### Why

  
  

### What

Both `ActionView`  and `ActionController` has `render` method.

- [render]((https://api.rubyonrails.org/classes/ActionController/Rendering.html#method-i-render))
- [render]((https://api.rubyonrails.org/classes/ActionView/Helpers/RenderingHelper.html#method-i-render)) this one has `render formats: [:json, :html]`, as search `:formats` in the [source code](https://github.com/rails/rails/blob/main/actionview/lib/action_view/lookup_context.rb#L18)

It's confusing the [documentation](https://guides.rubyonrails.org/layouts_and_rendering.html) mix those two methods together.

  
  

### How

  
  
  

### Where

  
  

### When

  
  
  

### Who