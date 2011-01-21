---
layout: post
title: Ruby File append mode
date_string: 21 January 2011
---

There are different file modes available to the developer when creating and opening new files in Ruby. One that I didn't know about was "a" which basically means append to the end of the file rather than starting a new one. What could it be useful for? One example would be as a log file of some sort where one wants to preserve the old data and add new data to the end of the file. Very trivial but helpful if you know about these things. Just makes you a better developer.

A simple code example would be:

<pre>
    file = File.new("datamapper.log", "a")  
</pre>