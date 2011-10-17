--- 
layout: post
title: Immediate Values
date_string: 31 October 2009
---

In a <a href="http://www.ploughthroughruby.co.uk/2009/08/is-variable-an-object/">previous post</a>, I have explained that variables are basically passed by values in ruby but since they have a reference to the original object any mutator methods can bascially modify the object itself. However, there are two exceptions to this; Fixnum and Symbol. 

Both, Fixnum and Symbol, store the values and have no reference to the object. This also applies that there are no mutator methods for Fixnum and Symbol and they are immutable. So, how can we actually prove this fact. Let us do a simple experiment and I think I might have done this before but I do not want you going back and forth between posts so let us just do it again. Run the code snippet and we are going through each step:

<pre>
  fixnum_1 = 3
  p fixnum_1.object_id
  fixnum_2 = 3
  p fixnum_2.object_id
  str_1 = "3"
  p str_1.object_id
  str_2 = "3"
  p str_2.object_id
</pre>

You will see that both the fixnum variables have the same object_id where as with str variables they will be different. So, what does that mean? It simply means that two fixnums of same value always represent the same object instance, so instance variables for Fixnum with value 1 are shared across the system. The same is the case with Symbol.

Ok. Fine. This makes perfect sense but why should I bother with all this explanation. Well, that is a million dollar question really and the answer to that is "You can't define singleton methods on Fixnums and Symbols". What? Why? I know this is confusing but when in doubt think of an example. 

We previously established that all the fixnum variables with same value are actually pointing to the same object instance. If let us say I want to define a singleton method on one then it would really define the singleton method on that object instance which means all the fixnum variables with same value would really share that new method you have added. Therefore, in order to cut that possibilty out one cannot define singleton methods on Fixnum, and Symbls.

Update: I have just realised that true (TrueClass), false (FalseClass) and nil (NilClass) also store the references as immediate values. And, yes there is a TrueClass, FalseClass and NilClass and true, false and nil are singleton instances of these classes.
