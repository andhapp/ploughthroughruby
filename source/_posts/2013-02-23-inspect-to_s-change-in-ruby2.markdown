---
layout: post
title: In Ruby2, inspect independent of to_s 
date_string: 23 February 2013
---

[Ruby 2.0.0](http://www.ruby-lang.org/en/news/2013/02/24/ruby-2-0-0-p0-is-released/) has been released and there are a lot of new things, for example, keyword arguments, TracePoint API, DTrace and so on. Here's [Ruby NEWS](https://github.com/ruby/ruby/blob/trunk/NEWS) file, and some [new features in Ruby 2](http://blog.marc-andre.ca/2013/02/23/ruby-2-by-example/).

One thing to add to that list is that the behaviour of inspect is no
longer dependent on to_s. In Ruby 1.9, if to_s was overridden inspect
would just execute that code. But in Ruby 2.0, to_s overriding doesn't
affect inspect anymore. Here's code example for [Ruby 1.9.3](https://eval.in/11121) and [Ruby
2](https://eval.in/11120)
