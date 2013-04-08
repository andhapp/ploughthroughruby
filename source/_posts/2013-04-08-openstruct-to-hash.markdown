---
layout: post
title: OpenStruct to hash
date_string: 8 April 2013
---

OpenStruct is a handy class in ruby's stdlib. I've used it in the past
for creating test data, instead of using factory girl. It's fast, and
the fact that it behaves like a Hash, makes it super easy for stubbing
object behaviours.

The other day, I had this requirement to convert an open struct instance
into a hash. I foolishly tried to_hash call, considering that it acts as
a hash, so there must be a to_hash call on it. But, unfortunately, there
isn't any to_hash methods on OpenStruct. However, there are other ways
to convert an open struct instance to a hash quite easily. Here's how:

### Option 1  
<pre>
os = OpenStruct.new(:id => 12)
os.marshal_dump # returns the hash {:id=>12}
</pre>

### Option 2
<pre>
os = OpenStruct.new(:id => 12)
os.instance_variable_get(:@table) # returns the hash {:id=>12}
</pre>
