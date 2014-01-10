---
layout: post
title: Abbreviation in Ruby
date_string: 10 January 2014
--- 

Ruby's standard library is filled with several unique, non-standard classes/modules, one such module is [Abbrev](http://ruby-doc.org/stdlib-2.1.0/libdoc/abbrev/rdoc/Abbrev.html).

Abbrev calculates the set of unique abbreviations for a given set of strings. The following code demonstrates it properly:

```
require 'abbrev'
require 'pp'

pp Abbrev.abbrev(['ruby', 'rules'])
```

This code produces the following output where all the keys are
abbreviated and unique, and point to their respective words.

```
{"ruby"=>"ruby",
 "rub"=>"ruby",
 "rules"=>"rules",
 "rule"=>"rules",
 "rul"=>"rules"}
```

This also provides an extension for an Array, so you can call 'abbrev'
method straight on an array. The code above will then become:

```
require 'abbrev'
require 'pp'

pp ['ruby', 'rules'].abbrev
```

I found a couple of use cases of the Abbrev module on Google:

1. For creating [unique labels](http://www.aimred.com/news/developers/2010/05/11/rediscovering_ruby_abbrev/) for a bar graph.

2. For creating an [auto-completer](http://endofline.wordpress.com/2010/12/25/ruby-standard-library-abbrev/) on console, intriguing, right? 

Hope this will make you aware of such a nifty module and please share your
use-cases with the rest of us.
