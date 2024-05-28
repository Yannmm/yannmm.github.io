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

- "One step right then up" is how Ruby try to locate a method in the ancestors chain. "One step right" means find the class of the instance; while "up" means trace up ancestors chain.

- [Module#refine](https://docs.ruby-lang.org/en/master/Module.html#method-i-refine) can add methods to existing module. What's more interesting, that change is not effective immediately. We need to call [Module#using](https://docs.ruby-lang.org/en/master/Module.html#method-i-using) to make it effective in current module / class context (or end of file if called at the top level). This is a good way to avoid global `Monkeypatching`. It has higher precedence thant open `class`.

### How

  
  
  

### Where

  
  

### When

  
  
  

### Who