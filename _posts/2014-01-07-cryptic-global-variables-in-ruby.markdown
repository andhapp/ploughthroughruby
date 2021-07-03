---
layout: post
title: Cryptic global variables in Ruby
date_string: 07 January 2014
--- 

Do you know what $! means in Ruby? 

Years ago, I was discussing some issue regarding GemCutter (now that makes
it ancient in programming age), and we were talking about global
variables in Ruby, for example, $; and $/. At the time, we couldn't
really find a place to look them up, even Google [isn't very effective](https://www.google.co.uk/search?q=%24!+Ruby&oq=%24!+Ruby&aqs=chrome..69i57.2487j0j7&sourceid=chrome&espv=210&es_sm=91&ie=UTF-8) given 
the nature of the query.

Anyways, while looking through Ruby's standard library, I found the file
[English.rb](http://ruby-doc.org/stdlib-2.1.0/libdoc/English/rdoc/English.html). 
This library has English names for all the cryptic global variables. For
example: $ERROR_INFO represents $!.

If you ever have to look up the English names, which I suggest you do as
it makes code easier to read, just refer to that file.
