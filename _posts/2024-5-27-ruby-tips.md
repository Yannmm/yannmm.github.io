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

- All below methods turn a block into a `Proc`:

    ```
    p1 = Proc.new { |a, b| [a, b] }
    p2 = lambda { |a, b| [a, b] }
    p3 = ->(a, b) { [a, b] }
    
    def do_math(a, b, &op) // Turn block into proc
        math(a, b, &op) // Turn proc into block
    end
    ```

- `Proc` vs `Lambda`. a> `return`: lambda returns from its scope, behaves just like normal method; proc returns from the scope where itself is defined. b> `arity`: lambda is less tolerant than proc when it comes to arguments. Calling with wrong number of arguments will render lambda with `ArugmentError` while proc fits the argument list to its own expectations.


- Seems `lambda` is more intuitive than procs because they're more similar to methods.


- The `Callable Objects` family: 

### How

  
  
  

### Where

  
  

### When

  
  
  

### Who