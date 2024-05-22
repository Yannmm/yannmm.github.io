---

layout: post

title: "Mystery Resolved: The Ruby "===" (Case Equality) Operator"

tags: rails ruby

---


  

### Why

Today while read source code of `Grape` gem, I spot an interesting line:

```
Hash === options
```

This makes me wonder what is `===` and how it works.

There seems serval "Equality" method in Ruby. So after some Googling, I find a [stack-overflow answer](https://stackoverflow.com/questions/7156955/whats-the-difference-between-equal-eql-and) that states difference among them. It seems to be the `Case Euqality` operator, most commonly used with `case...when` statements.

However, another things bugs me: This operator seems to can be called on `Class` object as well as instance object. How it that works?

To find out, I first look up the documentation. 

For [Object#===](https://docs.ruby-lang.org/en/master/Object.html#method-i-3D-3D-3D), it says:

> Returns  `true`  or  `false`. (1)
> Like  [`Object#==`](https://docs.ruby-lang.org/en/master/BasicObject.html#method-i-3D-3D), if  `object`  is an instance of  [`Object`](https://docs.ruby-lang.org/en/master/Object.html)  (and not an instance of one of its many subclasses). (2)
> This method is commonly overridden by those subclasses, to provide meaningful semantics in  `case`  statements. (3)
  
I have no problem with sentence 1, the returning value part. For sentence 2, I don't quite get its meaning. Then for sentence 3, I guess it means Subclasses may define custom behavior for their instances. So there is no mentioning how this operator is used with Class objects.



### How

With confusion bore in my mind, I read some good articles explaining Ruby inheritance hierarchy and the `===` operator. But none of them answer my question.

Then I read the `Object#===` documentation again and finally have a clue in my mind.

Sentence 2 can be rephrased like this: If `self` is an instance of Object, then this operator works just like [Object##](https://docs.ruby-lang.org/en/master/BasicObject.html#method-i-3D-3D), which is "pointer comparison".

For sentence 3, since [Class](https://docs.ruby-lang.org/en/master/Class.html) is a descendent of `Object`, it should be able to have custom behavior.

The inheritance chain of `Class` is: [Class, Module, Object]. And finally I found the explanation of [Module#===](https://docs.ruby-lang.org/en/master/Module.html#method-i-3D-3D-3D):

> Case Equality—Returns `true` if _obj_ is an instance of _mod_ or an instance of one of _mod_’s descendants. Of limited use for modules, but can be used in `case` statements to classify objects by class.


### What

As a Ruby beginner who comes from C like language, I always found it' confusing that many method can be called on instances of Classes as well as Classes themselves. You cannot just tell whether a method is class level or instance level easily. 

So my conclusion is: There is no such difference regarding class or instance method. They are only instances, either born from `Class` or from some other classes. A method can be called on Class directly if you include it into `Class`. If included into class of an instance, then it's available for instances.
  
  

### Where



  
  

### When

  
  
  

### Who