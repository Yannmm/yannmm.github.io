---
layout: post
title: Ruby Gotchas
tags: ruby
---

In this post I note down some of the Ruby's tricks and magics which confuses me easily.


### Splat Operator

In method definition, the splat operator `*` does two things opposite of each other.

When used with parameter, it `constructures` arbitrary number of arguments into an array; while used with argument, it `destructures` the array into arguments.

```
class Test
  def self.perform(*args)
    new(*args).perform
  end

  def initialize(x, y, z)
    ...
  end
end

Test.perform(1, 2, 3)

```

**Reference**: [Ruby splat operator 🌟](https://thoughtbot.com/blog/ruby-splat-operator?utm_source=pocket_shared)