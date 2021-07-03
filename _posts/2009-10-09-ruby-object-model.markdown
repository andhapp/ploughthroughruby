--- 
layout: post
title: Ruby object model
date_string: 09 October 2009
---

Right, so you know Ruby's object model. Well here's a little code snippet by JRuby creator Ola Bini and it drives the point home really.

<pre>
class Obj
  def something
    puts "calling simple"
    @abc = 3*42
    def something
      puts "calling memoized"
      @abc
    end
    something
  end
end

o = Obj.new
o.something
o.something
o.something

</pre>
The output of the code is:

<pre>
calling simple
calling memoized
calling memoized
calling memoized
</pre>

Let us look at the code and anaylise it. 'o' is an instance of 'Obj' class. 'something' is an instance method of 'O', therefore it can access it. The first 'o.something' would call the instance method defined in 'Obj' class. So, it prints "calling simple" and then the second 'something' defines a method on instance 'o' because inside the first 'something' self is same as instance 'o'.

Now, what do you get when you do something like this:

<pre>
def o.something
     puts "I am o's singleton method."
end
</pre>

Yes, you get a singleton method on the instance. In this case, that's exactly what happens. The second 'something' defines a singleton method on instance 'o'.  We are still in the middle of executing the first something. The last line of the first something (or the outer something) calls the method 'something'. What the hell? Cyclic messaging!!!! Never ending loop. Yeah, but the code runs and exits gracefully.

Well, the call to 'something' would actually go and look for 'something' method and before it finds a 'something' method defined in the class 'Obj' it would find the singleton-method 'something' and execute that. So, what would that print. Yeah, you are right it prints "calling memoized". The second and third calls to something will again encounter the 'something' singleton method and execute that and it would not bother to go and look for the something defined as an instance method in class 'Obj'.

I know you are confused. Why would it go and look for the singleton method and not the instance method. This is the magic behind Ruby's object model. Please head over to Ola Bini's blog and read the article on <a href="http://ola-bini.blogspot.com/search/label/metaprogramming">metaprogramming</a>. He goes into a lot more detail.
