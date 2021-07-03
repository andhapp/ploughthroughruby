--- 
layout: post
title: Ruby idioms
date_string: 24 September 2009
---
You can write a complete ruby script as a string and run it. Ruby (rather MRI) would just evalutae the string by executing it. For example:

<pre>
"#{def x(s); puts(s.reverse); end; ('1'..'3').each{|aStr| x(aStr)} }"
</pre>

This is absolutely valid.
