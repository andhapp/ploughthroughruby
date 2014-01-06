---
layout: post
title: Nested exceptions in Ruby 2.1.0
date_string: 06 January 2014
--- 

With Ruby 2.1.0, one can easily trace the original exception.
Previously, on rescuing an exception one would have no reference to the original exception
(thrown by a gem/library). There are a couple of [gems](https://github.com/skorks/nesty) that can help you
keep track of the exceptions, but with Ruby 2.1.0 you can work with
nested exceptions without any issues. Here's some trivial code to
achieve the same:

```
class Car
  def self.start
    begin
      1/0
    rescue => ex
      puts "Exception: #{ex}"
      raise StandardError.new "Can't start the car"
    end
   end
end

begin
  Car.start
rescue => ex
  puts "Cause: #{ex.cause}"
  puts "Exception: #{ex}"
end
```

This will produce the following output:
```
Exception: divided by 0
Cause: divided by 0
Exception: Can't start the car
```

You can [play around](https://eval.in/86466) with the code yourself.
It's not as sophisticated as the gems out there, but it's getting there.
