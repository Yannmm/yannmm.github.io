---

layout: post

title: Rest-like API Framework: Grape

tags: rails ruby grape

---

### What

Rails alone is of course capable of acting as an API-only application. But Grape did a better job, said my colleague.
  

### Why

Grape is designed to build Rack-compliant application that can run on Rack or on existing web application, like Rails.

To work with Rails, we [mount](https://api.rubyonrails.org/classes/ActionDispatch/Routing/Mapper/Base.html#method-i-mount) Grape API entrance in the `route.rb` file. You may ask since Grape can do the API job alone, why bother to run it on a Rails application? My best guess is that  this way will enable us to utilize many conventions that Rails provide, like the way to name and organize files and classes, other supportive Rails gems, etc.


 
### How

Grape enable us to define API declaratively, with its own DSL. This bugs me a lot. Since a beginner, I thinks Ruby's grammar is too flexible to comprehend. This is getting way worse when arrived at Grape.

E.g, for below code, how params are associated with each route?

```
class  Headers < Grape::API
	format :json
	
	namespace :headers do
		desc 'Returns a header value.'
		params do
			requires :key, type: String
		end

		get ':key' do
			key = params[:key]
			{ key => headers[key] }
		end

		desc 'Returns all headers.'
			get do
				headers
			end
	end
end
```

I guess Grape will smartly wrap `params`, `desc` and other configurations into next closest `route`. A formula like this:

```
Endpoint = Route + ParamsScope + ...
```

Check [here](https://www.rubydoc.info/github/ruby-grape/grape/master#Routes) for how to define Route.

And luckily, I have `ChatGPT` to explain code for me, which is very helpful.

  


### Where

  
  

### When

  
  
  

### Who



