---

layout: post

title: Ruby Tips

tags: ruby

---

  

  

### Why

  
  

### What

- The keyword `class` is actually an operator in Ruby. It open a tunnel connecting to the scope of a certain object, where you can do stuffs like adding instance methods.

- Constants are references as well. So they can be changed to refer to something else.

- Any reference beginning with an uppercase letter are Constants, including classes and modules. They are arranged  in a tree similar to the linux file system, where modules and classes are directories and constants are files. The constant path uses `::` as separator.

- A leading `::` stands for root.


- `Anonymous Module` means a module with no name assigned. It's used in [Kernel#load](https://docs.ruby-lang.org/en/master/Kernel.html#method-i-load). We can create one like this:

    ```
        anonymous_module = Module.new do 
            def greeting
                "Hello from another module"
            end
        end
    ```
  
  
- `include` a module will append that module after the including class in the `ancestors` chain; while `prepend` will insert that module before the including class in the chain.


- To define instance method, both `def` keyword and [Module#define_method](https://docs.ruby-lang.org/en/master/Module.html#method-i-define_method) serve the same purpose. But the latter let you determine the method name until runtime.

- Ruby's `Object Model` is fanscinating: both instance and class are all objects. class has `instance_methods` while `Class`'s instance_methods are called on class.

- `Callable objects` include procs and lambdas. Blocks are convertible to them.

- Just like method, a block returns the result of the last line of code it eveluates. Block vs Closure???

### How

  
  
  

### Where

  
  

### When

  
  
  

### Who