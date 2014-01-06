---
layout: post
title: Aspect Oriented Programming
date_string: 30 December 2013
---

I was looking into Ruby's [TracePoint](http://www.ruby-doc.org/core-2.0.0/TracePoint.html) class recently. TracePoint is an objectified Kernel#set_trace_func method. TracePoint was 
added in Ruby2, but before that there was a gem that had same function as TracePoint
class. Surprisingly, it was also called [tracepoint](https://github.com/rubyunworks/tracepoint).

Anyways, TracePoint is not the scope of this post. This post is all about AOP,
or Aspect Oriented Programming. 

Wikipedia defines it as *"aspect-oriented programming (AOP) is a programming paradigm that aims to increase modularity by allowing the separation of cross-cutting concerns. AOP forms a basis for aspect-oriented software development."*

There are couple of things worth noting, Modularity and Cross-cutting concerns.

### Modularity

In English, Modularity means based on modules, easily assembled, or repaired 
and the reason it's easily repaired is because modules are
self-contained and talk to each other via a defined interface. Interface
could be hardware pins, RAM slots, or intangible ones, defined in your
Ruby or Java class. 

In Ruby world, modules and modularity is the go-to thing to achieve
separation of concern. You got a piece of code that is used in two
different places and has no state of its own, just create a
module to be included/extended or prepended.

### Cross-cutting concerns

Cross-cutting concern can be defined as any piece of code that's more widely 
used across the application, for example, logging, security, or authentication, perhaps. 
Something, like a before_filter in Rails controllers that's applied to a set of actions.

There are libraries that one could use to achieve same and even more
than before_filter functionality outside of Rails. The one that I
briefly looked at is called
[Aspector](https://github.com/gcao/aspector). It provides a lot of examples
as well just in case you are stuck.

### Why not just use Ruby Modules?

Ruby modules are similar but not exactly same as the AOP concept. One
important difference is that you can apply an aspect (aspect is the
piece of code with common functionality, like a module) to a class from
outside, without opening the class. Here's some aspector code snippet to
elaborate the point:

<pre>
TestAspect.apply A
</pre>

Here A is the class, and TestAspect is the aspect. As you can see, you
can just apply it from outside. Sorry, not very clear, but I didn't want
to tie the concept to a particular library implementation.

One good use case of using AOP concepts would be with something like
debugging, for example, a user performed an action and you want to check
the log for parameters that are getting passed in to methods, or what
methods are getting called when certain action is performed. But, that's
what TracePoint does, right? Well, it definitely allows one to hook into
the events and print debugging information. With AOP, one can create
more focussed debugging. Imagine, a request going through Rails stack
will hit a lot of methods and you don't want to enable tracing and then
having to go through a long console output. 

These are just some of the initial thoughts I had on reading AOP and TracePoint. 
Hope this post will encourage you to investigate and learn more about these topics.

