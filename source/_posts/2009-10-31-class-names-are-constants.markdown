--- 
layout: post
title: "Class names are constants "
date_string: 31 October 2009
---

Ruby is an object oriented programming. Let us look at a code sinpet:

<pre>
 str =  String.new("ruby rocks")
</pre>

So, we define a variable called "str", which stores a pointer to the object created by sending "new" on "String". Here, "String" receives the "new" message but for "String" to take any action when it receives "new" message it must have a reference to the object called String. Therefore, there must be a corresponding constant to every class in ruby. It can't be a variable as it starts with an uppercase. 

Actually, that is exactly what happens. Every class in ruby has a global constant which stores a reference to the object and is used for method invocations. So, there are two things really one is the constant named String and the other is the object named String.
