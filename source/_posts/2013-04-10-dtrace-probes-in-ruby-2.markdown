---
layout: post
title: DTrace probes in Ruby 2 and a startling discovery
date_string: 10 April 2013
---

DTrace is a static and dynamic instrumentation framework. I did a talk
at LRUG back in October on DTrace and it's addition in Ruby 2. There's
not much content in the presentation, but it will give you a little
pointers to the present situation of DTrace in general, and in Ruby.

The more I look into DTrace, the more I find it intriguing, challenging,
surprising, and yet thoroughly enjoyable. Recently, I was refactoring some 
of the tests for a project, and the test suite takes forever to run,
therefore, I decided to use Object.new for creating an instance of the
interested object (stub the requests). Another colleague came along and
commented..."Oh, why are you not using OpenStruct". OpenStruct is handy,
as it has a hash like structre, which means a method call that hasn't
been stubbed or instantiated will just return nil, just like a hash call
when the key is absent from the hash.

I ran some quick benchmarks and here are the results:

<pre>
Calculating -------------------------------------
         Struct.new       7341 i/100ms
         Object.new      57600 i/100ms
     OpenStruct.new       5462 i/100ms
-------------------------------------------------
         Struct.new     90353.5 (±10.0%) i/s -     447801 in   5.017170s
         Object.new   2335283.3 (±3.2%) i/s -   11692800 in   5.012149s
     OpenStruct.new     65014.7 (±4.9%) i/s -     327720 in   5.053209s
</pre>

One thing is obvious, if you don't need the dynamic nature of an
OpenStruct, just use Object.new. This led me to think, why Object.new is
superfast as compared to Struct or OpenStruct. I wanted to see what
method calls is Struct or OpenStruct making, you know, just for my own
knowledge. I decided to use DTrace for that purpose. DTrace has been
added to Ruby 2, but I still couldn't find any documentation. However, 
[probes.d](https://github.com/ruby/ruby/blob/trunk/probes.d) file gives
a details of all the probe names, arguments in the probe and so on.
Please look at that file if you'd like to use DTrace with ruby.

I created a simple ruby file called `test.rb`, like this:

<pre>
Object.new
</pre>

and ran the following dtrace command on a Mac OS X:

<pre>
sudo dtrace -c 'ruby test.rb' -Zn 'ruby*::method-entry { @[copyinstr(arg0)] = count(); }'
</pre>

to receive the following output:

<pre>
dtrace: description 'ruby*::method-entry ' matched 2 probes
dtrace: pid 14009 has exited

  Gem                                                              12
  Gem::Requirement                                                 23
  Gem::Version                                                     36
  Gem::Specification                                              267
  RbConfig                                                        309
</pre>

Here column 1 is the Class name and the column 2 is the number of
times that class was accessed while running this ruby file. This was
quite surprising that RbConfig was accessed 309 times. Why? After much
thinking, I thought may be RVM has got a hand in this. I haven't found a
solution yet.

I leave you here with this startling discovery and hope to solve
it for my next post. I'm planning to run the same dtrace command with
ruby installed via rbenv and see what I get and then go from there.











