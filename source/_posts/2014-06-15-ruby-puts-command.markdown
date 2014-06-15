---
layout: post
title: Ruby puts command
date_string: 15 June 2014
--- 

Ruby's puts command will lead the 'most used command' competition in the language. It's probably the first command you run when you fire up irb, or write HelloWorld.rb. I have been using it from day 1, for debugging, printing out the progress of long running scripts and so on. I recently found couple of nifty things you can do with puts command:

* You can pass it multiple arguments and it will print them on the screen with a line break, for example:

<pre>
irb(main):001:0> puts "First", "day"
First
day
=> nil
</pre>

* Secondly, you can pass it an array of elements, and it will print the elements with a line break, for example:

<pre>
irb(main):004:0> puts ["Second", "Day"]
Second
Day
=> nil
</pre>

Hope you can use this to replace multiple calls to puts in your code.
