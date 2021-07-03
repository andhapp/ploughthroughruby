---
layout: post
title: An Interesting Ruby Method
date_string: 17 April 2011
---

In this post, I will talk about a ruby method that I had no idea existed which might come handy in debugging your code.

The method I am talking about is *set_trace_func*. It's part of the Kernel class and it does what it says. Allows one to set the method tracing on a method. The following snippet explains it further. Here, we have a class, TestingSetProcFunc:

<pre>
    class TestingSetProcFunc
      def traceThisMethod
        source = 1
        target = 2
      end
    end
</pre>

To inject set_trace_func in, it needs to be called before the method is invoked, like this:

<pre>    
    puts "Event    File:Line                Id          Binding        Classname"
    set_trace_func proc { |event, file, line, id, binding, classname|
      printf "%8s %s:%-2d %20s %12s %8s\n", event, file, line, id, binding, classname
    }
</pre>

It takes a proc with upto 6 arguments. These are the events with their brief descriptions: 

* c-call (call a C-language routine)
* c-return (return from a C-language routine)
* call (call a Ruby method)
* class (start a class or module definition)
* end (finish a class or module definition)
* line (execute code on a new line)
* raise (raise an exception)
* return (return from a Ruby method).

Now, to run this we just need to call the method and look at the output:

<pre>
    tracer = TestingSetProcFunc.new
    tracer.traceThisMethod
</pre>

This is what the output will look like when you run it on the command line:

<pre>    
Event    File:Line                Id          Binding        Classname
c-return test.rb:11       set_trace_func #<Binding:0x0b53c4>   Kernel
    line test.rb:13                      #<Binding:0x0b52fc>         
  c-call test.rb:13                  new #<Binding:0x0b525c>    Class
  c-call test.rb:13           initialize #<Binding:0x0b5144> BasicObject
c-return test.rb:13           initialize #<Binding:0x0b5090> BasicObject
c-return test.rb:13                  new #<Binding:0x0b4ff0>    Class
    line test.rb:14                      #<Binding:0x0b4f50>         
    call test.rb:2       traceThisMethod #<Binding:0x0b4eb0> TestingSetProcFunc
    line test.rb:3       traceThisMethod #<Binding:0x0b4dfc> TestingSetProcFunc
    line test.rb:4       traceThisMethod #<Binding:0x0b4d5c> TestingSetProcFunc
  return test.rb:5       traceThisMethod #<Binding:0x0b4cbc> TestingSetProcFunc    
</pre>

This output gives one a good idea about the work that is happening in the background. The weird looking Binding instance is the context at that particular place in the code. I have just scratched the surface and I am sure there's a lot one can do with this method. Have a look at the [ruby's test for set_trace_func](https://github.com/ruby/ruby/blob/trunk/test/ruby/test_settracefunc.rb) for more useful ways of employing it.
