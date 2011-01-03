--- 
layout: post
title: Convert Array to Hash mystery
date_string: 02 January 2011
---

It is always easy to find solutions on Google but the real fun is in finding out how a bit of code works. It just helps you understand much more about the language and how it behaves. Converting an array to hash is easy. Just use this piece of code that I found on google:

<pre>
  some_array = [1,2,3]
  some_hash = Hash[*(some_array.collect{|v| [v,v]}.flatten)] # yields {1=>1, 2=>2, 3=>3}
</pre>

Few people have asked the question behind this conversion and I just decided to break it apart and tackle it bit by bit. Our objective, again, is to convert an array to a hash. Hash's ruby documenation tells us that a new Hash object can be created by using even number of arguments. Something similar to the following code:

<pre>
  some_hash = Hash[1,1,2,2,3,3] # This creates a hash object similar to this {1=>1, 2=>2, 3=>3}
</pre>

All we need to do now is convert our some_array (defined in the first code snippet) and convert it into [1,1,2,2,3,3].

It's simple really. We take the some_array and convert it into an array's or array like this:

<pre>
  some_array = [1,2,3]
  some_array.collect{|v| [v, v]} # will yield [[1,1], [2,2], [3,3]]
</pre>

Now to convert it into [1,1,2,2,3,3] we just need to flatten this array of arrays like this:

<pre>
  some_array = [1,2,3]
  some_array.collect{|v| [v, v]}.flatten # will yield [1,1,2,2,3,3]
</pre>

Now, all we need to do is use the splat (*) unary operator. The splat operator expands the supplied array into individual arguments which is what we need to convert array into a hash. You could also achieve the same with the following snippet:

<pre>
  some_array = [1,2,3]
  some_hash = Hash[*(some_array+some_array).sort] # yields {1=>1, 2=>2, 3=>3}
</pre>

I hope you can work that out yourself. I hope this little discussion helped you.
