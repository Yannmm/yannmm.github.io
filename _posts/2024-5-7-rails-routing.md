---

layout: post

title: Rails Routing

tags: rails ruby

---


  

### Why


  

### What

One interesting fact, for [namespace](https://api.rubyonrails.org/v7.1.3.2/classes/ActionDispatch/Routing/Mapper/Scoping.html#method-i-namespace) and [scope](https://api.rubyonrails.org/v7.1.3.2/classes/ActionDispatch/Routing/Mapper/Scoping.html#method-i-scope):

```
namespace :test do
	resources :cars, only: :index
end

# Equals to

scope :test, as: :test2, path: :test2 do
	resources :cars, only: :index
end
```
 
 By the way, for `scope` with `module`  set explicitly and `namespace` whose `module` is set implicitly. A module is automatically defined:

```
Module Test
end
```
  

### How

  
  
  

### Where

  
  

### When

  
  
  

### Who