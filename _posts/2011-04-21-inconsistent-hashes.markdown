---
layout: post
title: Inconsistent hashes
date_string: 21 April 2011
---

To clarify, hashes here does not mean the Hash class. Object's in ruby have a hash method that returns a hash code for an object. The hash is also used in the background by the eql? method. So, it's safe to say that two objects are equal if their hash methods return the same value.

Now, carry out a simple exercise and see what happens. Fire up an IRB session and run the following code, one by one:

<pre>
    "test".hash
    1.hash
    [].hash
</pre>

And note the output after every command run. Now, exit out of IRB and start a fresh session and run the same piece of code again. This time you will see the hash values have changed completely. This might be a bit surprising but it has been implemented in Ruby 1.9 for security reasons as it avoids one from guessing hash values. I picked this up from Ruby-core ML discussion and hope you find it useful.