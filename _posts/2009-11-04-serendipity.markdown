--- 
layout: post
title: Serendipity
date_string: 04 November 2009
---

I accidently found a nifty way of calling <del datetime="2009-11-04T09:19:06+00:00">class</del> singleton methods. Imagine you have this code:

<pre>

class FoundANewWay
    def self.to_call_a_singleton_method
        puts "It works!"
    end
end
</pre>

and you can call it like this:

<pre>
FoundANewWay.to_call_a_singleton_method

or

FoundANewWay::to_call_a_singleton_method
</pre>

Cool!
