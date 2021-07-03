
---
layout: post
title: Use Sequel for non-rails ruby apps
date_string: 14 September 2016
---

I am writing a ruby script to retireve some data via HTTP call and then add it to the database.

Now, I decided to use ActiveRecord as an ORM and wrote a [gem](https://github.com/andhapp/activerecord_sans_rails) for the same.

Nothing complicated. It's just a Rakefile that provides popular activerecord rake tasks.

But, then I stumbled across blog post on [Sequel](https://www.toptal.com/ruby/api-with-sinatra-and-sequel-ruby-tutorial) and I feel
Sequel is a better choice for an ORM for a non-rails app.

Why?

Because, Rails is opinionated.

And it's nuances works nice for a Rails app.

Anything outside of the realms of a standard Rails app and all bets are off.

It is like fitting a square peg in a round hole. It's possible but you will have to shave off the extra bits.

Sequel on the other hand seems like a better fit for a ruby script.

Will post my experience with Sequel. It has ample documentation and the project was last updated on 16th September 2016.
There are no outstanding pull requests or issues on github which implies the project is active and nicely looked after.
