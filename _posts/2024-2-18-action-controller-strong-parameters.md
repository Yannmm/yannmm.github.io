---
layout: post
title: Action Controller Strong Parameters
tags: rails
---

### Why
It's forbidden to use raw parameters of `ActionController` for mass-assignment to `Active Model`. Developers have to consciously choose which fields are allowed.  This is a better security practice to help prevent accidentally allowing users to update sensitive model attributes.

### What

The `params()` instance method of `ActionController` will return a `ActionController::Parameters` object, carrying the request's parameters.

- @see https://api.rubyonrails.org/v7.1.2/classes/ActionController/StrongParameters.html#method-i-params

### How

`ActionController::Parameters` provides two methods: `require` and `permit`. The former is used to mark parameters as required. The latter is used to limit which attributes should be allowed.

- @see https://api.rubyonrails.org/v7.1.2/classes/ActionController/Parameters.html#method-i-require

- @see https://api.rubyonrails.org/v7.1.2/classes/ActionController/Parameters.html#method-i-permit

### Where

This parameters sanitization process happens at `ActionController.` Usually is private method is defined to encapsulate the permissible parameters

```
class PeopleController < ActionController::Base
	# some public actions
	
	private
	def person_params 
		params.require(:person).permit(:name, :age)
	end
end
```

### When

Parameters sanitization can be achieved:
- in the `before_action`, or
- in the action method


### Who

Pending
