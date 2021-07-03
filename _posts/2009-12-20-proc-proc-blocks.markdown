--- 
layout: post
title: Proc, proc, blocks
date_string: 20 December 2009
---

I know you must be thinking proc and Proc is the same thing and I must have mistyped. But, proc and Proc are different things. Blocks is a beautiful concept and you can achieve so much by using blocks carefully that it is unbelievable. I created a simple DSL using blocks and Faker gem to spit out XML used for testing purposes. I mean it took me few hours to do the first version up and running in Sinatra. Amazing.

So, block is nothing more than bits of code within curly brackets. The concept of blocks is used excessively throughout Ruby in iterators like inject, select, map, each and so on and so forth. For example:

<pre>
def example_from_a_block
  puts "Should call a block"
  yield 
  puts "Yes, I did!"
end
</pre>

and invoke it like:

<pre>
example_from_a_block { puts "in a block" }
</pre>

But blocks do have problems. Not exactly problems, but yeah shortcoming for sure. They are not objects. So...what difference does it make if they are not objects. I don't care man. I like them. Exactly you like blocks but you would love blocks wrapped as objects. Yes, these things do exist. They are called proc or lambda. So what is a proc then? It is basically a block but with object like features, I mean you can manipulate them and pass them around like regular objects. Cool. 

To create a proc, just do:

<pre>
p = Proc.new { puts "I am a proc" }
</pre> 

It is absolutely essential to pass a block to a proc. "p" is basically an instance of the class <a href="http://ruby-doc.org/core/classes/Proc.html">Proc</a>. Run this in you irb session and confim that it is indeed an object with an object_id:

<pre>
p.object_id
</pre>

Hmm...two down one to go. What exactly is a proc then. proc is just a simple global method, if you will, of the Kernel module. So, you can just invoke it like this:

<pre>
kernels_proc_variable = proc {|a| a + 10 }
</pre>

Now, proc behaves differently in Ruby 1.8 and Ruby 1.9. In 1.8, it returns a lambda where as in 1.9 it is a synonym for Proc.new. So, please be aware of this simple yet pivotal difference. Pivotal because lambda's and proc's are slightly different, although on the surface they look the same. They are both instances of Proc so let us just say they are siblings. There is so much more you can do with Procs and this post has just touched the surface of it. I will discuss lambda and closures in the coming posts and then compare them.
