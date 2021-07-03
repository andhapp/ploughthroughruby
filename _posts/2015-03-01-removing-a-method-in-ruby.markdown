---
layout: post
title: Removing a method in Ruby
date_string: 01 March 2015
--- 

There are several ways of adding a method to a ruby class (or instance),
for example, define_method, method_missing, or by just opening up the
class itself.

*However, can we remove the methods from a Ruby class?*

I encountered two ways of removing methods from a class:

* [remove_method](http://ruby-doc.org//core-2.2.0/Module.html#method-i-remove_method)

* [undef_method](http://ruby-doc.org//core-2.2.0/Module.html#method-i-undef_method)

There are subtle differences between the two. The former removes the
method from the current class, where as the latter, stops responding to
the methods in the current class.

Let's look at an example for the same. Imagine we have a parent class,
Appliance (a.k.a Kitchen Appliance), and child class, Can opener. Here
are the definitions for the two classes:

```
class Appliance
  def name
   puts "I'm a kitchen appliance"
  end
end

class CanOpener < Appliance
  def name
    puts "I'm a can opener"
  end
end

```

Now, let's try `remove_method` and see what happens.

```
can_opener = CanOpener.new
can_opener.name

class CanOpener
  remove_method :name
end

can_opener.name
puts "Can Opener has a name? #{can_opener.respond_to?(:name)}"   
```

This will produce the following output:

```
I'm a can opener
I'm a kitchen appliance
Can Opener has a name? true
```

As soon as you remove a method from a class it treats the method as
undefined and goes up the ancestor chain to look for an implementation, 
which it finds in the parent class. Since, there's an implementation 
`respond_to` returns true.

However, `undef_method` works slightly differently and let's see how:

```
class Appliance
  def name
   puts "I'm a kitchen appliance"
  end
end

class CanOpener < Appliance
  def name
    puts "I'm a can opener"
  end
end

can_opener = CanOpener.new
can_opener.name

class CanOpener
  undef_method :name
end
 
puts "Can Opener has a name? #{can_opener.respond_to?(:name)}"
can_opener.name
```

This will produce the following output:

```
I'm a can opener
Can Opener has a name? true
/tmp/execpad-f7201e261f52/source-f7201e261f52:21:in `<main>': undefined method `name' for #<CanOpener:0x41017dcc> (NoMethodError)
```

Unlike `remove_method`, `undef_method` stops responding to the method
and doesn't travel up the ancestor chain. It totally disregards the
method implementation in the parent class.

Quite interesting, however, I've never seen it used in any of the
production code before, so, hopefully, I will find a good use case for
it soon.



