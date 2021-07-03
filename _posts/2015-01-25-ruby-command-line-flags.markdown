---
layout: post
title: Ruby command line flag for debugging
date_string: 25 January 2015
--- 

Reading open source code is almost always a good idea. Open source code
has the benefit of being reviewed by a lot of committed users and it
just shows the good patterns of programming. For instance, I once
looked at Arel, and the code demonstrates an exemplary use of visitor
pattern. There isn't much code there, yet it manages to achieve so much.

Recently, I was reading some open source code recently and spotted $DEBUG
environment variable in quite a few places. At the time, I thought it
must be something the author used to simplify debugging. But, no, it's
defined and used by ruby core. Ruby provides a debug flag (-d or --debug) 
which when used would set the $DEBUG to true.

Try running the following script in irb, pry or whatever else you use:

```
ruby -d -e 'if $DEBUG; puts "Debugging"; end'
```

and you should see something like this as output:

```
RUBY_GC_HEAP_FREE_SLOTS=200000 (default value: 4096)
RUBY_GC_MALLOC_LIMIT=90000000 (default value: 16777216)
Exception `LoadError' at /Users/andhapp/.rvm/rubies/ruby-2.2.0/lib/ruby/2.2.0/rubygems.rb:1222 - cannot load such file -- rubygems/defaults/operating_system
Exception `LoadError' at /Users/andhapp/.rvm/rubies/ruby-2.2.0/lib/ruby/2.2.0/rubygems.rb:1231 - cannot load such file -- rubygems/defaults/ruby
Debugging
```

Don't worry about the two exceptions as in [debug mode exceptions are displayed](http://stackoverflow.com/a/1851232/20301) even when they are rescued.
