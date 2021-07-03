---
layout: post
title: Method default arguments and passing nil value
date_string: 03 January 2011
---

This is something very trivial and I kind of observed it whilst programming couple of weeks ago. For example, you had a method like this:

<pre>
  class SomeClass
    def some_method(some_argument = '')
      raise ArgumentError unless some_argument
    end
  end
</pre>


Now, I was under the impression that if I passed in a nil into this method, for some reason some_argument will still have the default value('') as opposed to the nil value passed in but default arguments come into play when no value is passed in for the method arguments. But I was passing in nil which is an instance of NilClass and therefore some_argument gets assigned the nil value and an exception is raised.
