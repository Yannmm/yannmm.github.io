---

layout: post

title: Ruby Exception Handling

tags: rails ruby

---

  

### Why

[Exception](https://docs.ruby-lang.org/en/master/Exception.html) packages error information, which is propagated back up the calling stack until a code block declaring how to handle that type of exception is found.

  
  

### What

The exception hierarchy is like:

```
	Exception
           NoMemoryError
           ScriptError
               LoadError
                   Gem::LoadError
               NotImplementedError
               SyntaxError
           SecurityError
           SignalException
               Interrupt
           StandardError
               ArgumentError
                   Gem::Requirement::BadRequirementError
               EncodingError
                   Encoding::CompatibilityError
                   Encoding::ConverterNotFoundError
                   Encoding::InvalidByteSequenceError
                   Encoding::UndefinedConversionError
               FiberError
               IndexError
				   KeyError
                   StopIteration
               IOError
                   EOFError
               LocalJumpError
               Math::DomainError
               NameError
                   NoMethodError
               RangeError
                   FloatDomainError
               RegexpError
               RuntimeError
                   Gem::Exception
               SystemCallError
               ThreadError
               TypeError
               ZeroDivisionError
           SystemExit
               Gem::SystemExitException
           SystemStackError
```
  
  

### How

The error handling structure is like:

```
begin 
	# Code that might throw exception
rescue ExceptionType1, ExceptionType2... => exception
	# handle error
rescue exception
	# Default to StandardError
	retry # Reexecute "begin" block
ensure
	# Code that always execute no matter error happens
end
```

With [Kernel#raise](https://docs.ruby-lang.org/en/master/Kernel.html#method-i-raise), you can either raise a [RuntimeError](https://docs.ruby-lang.org/en/master/RuntimeError.html) or any other types of exception, along with message and stack-trace.


  
  

### Where

  
  

### When

  
  
  

### Who

The `catch & throw` structure allows us to unwind the stack and continue to execute thereafter. Technically speaking, It's just like the `goto` statement in C. 

Here is an example:

```
word_list = File.open("wordlist") catch (:done) do
	result = []  
	while line = word_list.gets
		word = line.chomp  
		throw :done unless word =~ /^\w+$/ result << word
	end
	
	 puts result.reverse 
end
```