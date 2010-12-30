--- 
layout: post
title: Is variable an Object?
date_string: 17 August 2009
---

In Ruby, everything is an object. Well in Ruby 1.8, everything dervies from an Object. However, in 1.9 a BasicObject has been introduced which is a minimalist version of a full blown object.

Right, so is variable an object in Ruby?

The answer is "no". Let us look at the following code below and discuss what it does to reach a concrete solution. <br><br>

[gist id=169422]

<br><br>

This line basically creates a String object with the value "Tim" and stores it somewhere in the object heap. It then stores the reference of this object in the variable "person". Thus, a variable is not an object. It is a mere pointer to an object. In other words, variables hold references to the objects and not the objects themselves.

This is similar to how sometimes CPU registers work. Instead of storing the next instruction, the registers store the memory address of the next instruction.

<br><br>

<b>Update:</b>

Continuing this discussion, I would like to add that variables when passed to methods are passed by <em>value</em>. 

And? what does that mean?

Now, my contemporary Java and C developers (I like to call them geeks) would easily relate to the phrase "Pass by Value". When a variable is passed by value then the variable is copied to another location and that new temporary variable that is created is passed to the method. Let us say the code for that is something like the snippet below:<br><br>

[gist id=171321]

<br><br>

Going back to the Ruby World. In Ruby, the variables are passed by value but since these values are actually the references to the object means the method can modify the underlying object. Let us prove this simple phenomenon. Take the code above and fire up the Terminal (or cmd line for Windows) and type irb to start a new irb session and do the following:<br><br>

[gist id=171330]

and what do you see? Yeah that is correct they are the reference to the same object.
