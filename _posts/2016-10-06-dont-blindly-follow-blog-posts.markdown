
---
layout: post
title: Don't blindly follow blog posts
date_string: 06 October 2016
---

Technlogy changes fast!

And it's a blatant fact.

And with changing technology opinions, benchmarks and blog posts become obsolete, fast.

I was reading a blog post recently about adding some [performance related gems](http://marianposaceanu.com/articles/improve-rails-performance-by-adding-a-few-gems)
to improve rails's performace. It's a very nice, detailed article with benchmarks.

Instead of just blindly adding the suggested gems to the project, I ran the scripts again and found that:

* `escape_utils` gem makes things worse on `ruby 2.3.1` and `rails 5`, so no point in adding it.
* `fast_blank` gem, on the other hand, makes things slightly better, so definitely worth adding. With
slightly better I mean you are able to make more requests/sec.
* `je` and `jemalloc` gem didn't install for `ruby 2.3.1` at all.

Well, the point of this short blog post was to make you aware that blog posts go out of date and sometimes
it's necessary to re-evaluate the findings and ensure you are adding the gems for the right reasons.

Hope it helps!
