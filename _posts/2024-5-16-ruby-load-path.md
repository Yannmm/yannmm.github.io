---

layout: post

title: Ruby Load Path

tags: rails ruby

---
  

### Why

`Load path` simply refers to:

> Where to look for things.

For Ruby, global variable `$LOAD_PATH` is an array containing all the paths. It's defined when Ruby starts the program.

Check out this [article](https://webapps-for-beginners.rubymonstas.org/libraries/load_path.html) for a good basic explanation.

### What

  
  
  

### How

We can check the default load path of our Ruby installation with `ruby -e 'puts $LOAD_PATH'`.

```
/Users/rayman/.gem/ruby/3.1.2/gems/error_highlight-0.6.0/lib
/Users/rayman/.rubies/ruby-3.1.2/lib/ruby/site_ruby/3.1.0
/Users/rayman/.rubies/ruby-3.1.2/lib/ruby/site_ruby/3.1.0/arm64-darwin21
/Users/rayman/.rubies/ruby-3.1.2/lib/ruby/site_ruby
/Users/rayman/.rubies/ruby-3.1.2/lib/ruby/vendor_ruby/3.1.0
/Users/rayman/.rubies/ruby-3.1.2/lib/ruby/vendor_ruby/3.1.0/arm64-darwin21
/Users/rayman/.rubies/ruby-3.1.2/lib/ruby/vendor_ruby
/Users/rayman/.rubies/ruby-3.1.2/lib/ruby/3.1.0
/Users/rayman/.rubies/ruby-3.1.2/lib/ruby/3.1.0/arm64-darwin21
```

Notice, Rails application has way more paths than above.
  
  

### Where

When you call [require](https://docs.ruby-lang.org/en/master/Kernel.html#method-i-require) 'x', this is what happens:

1. If the file can be loaded from the existing Ruby $LOAD_PATH, load as it is.
2. Otherwise, installed gems are searched first file that matches. If it's found in gem 'y', that gem is added to the $LOAD_PATH.

When [require_relative](https://docs.ruby-lang.org/en/master/Kernel.html#method-i-require_relative) 'x' is called, Ruby tries to load the file relative to the directory containing the requiring file.

  

### When

  
  
  

### Who