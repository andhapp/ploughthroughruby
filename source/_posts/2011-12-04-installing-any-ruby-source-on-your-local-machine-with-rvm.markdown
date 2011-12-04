---
layout: post
title: Installing any Ruby source on your local machine with RVM
date_string: 04 December 2011
---

Now, if you are like me you probably have ruby source checked out on your machine to ensure that you stay informed with the newest features and ponder through the ruby source at will. I started wondering what if I want to install the ruby from the source and test my gems out and test it against well-known libraries to see how they fare. Firstly, I thought of doing the ./configure -> make -> make install dance but then I realised...yes you're absolutely right, why not use [RVM](https://github.com/wayneeseguin/rvm).

What RVM? I must be out of mind.

But, hey, RVM downloads ruby source code and installs it on your machine. The only difference is that I have got the ruby source checked-out on my machine and I want to use that as the source. And yes, RVM is awesome. I have spoken to [Wayne](https://github.com/wayneeseguin) (via IRC) and the man is an absolute genius, very polite and helpful.

So, somehow, I need to accomplish the following:

* Hey RVM, don't download the ruby source.
* Here's the location of the ruby source, use that and install it.
* Voila!

But, how do I do that? I started looking at RVM source code and I am not an expert at bash scripting, so I figured why not just mail RVM mailing list. I got the following helpful response from [Micheal Papis](https://github.com/mpapis). 

<pre>
it's not yet supported to use sources/rubies provided by user, but it
will be in rvm 2.0

as for using it now, you could use $rvm_path/src - and provide your
sources there ... not sure how it will work, you have to experiment a
bit
</pre>

That clue was enough for me and like he said, I experimented a little bit. When you run something like:

<pre>
rvm install ruby-1.9.2
</pre>

RVM downloads the source code into $rvm_path/repos, moves it over to $rvm_path/src and then does the configure, compile dance. I created a symlink in $rvm_path/repos pointing at the local ruby git repository on my machine. And, then I ran the install command. Here's the output I get:

<pre>
~/.rvm/src$ rvm install ruby-head
Installing Ruby from source to: /Users/andhapp/.rvm/rubies/ruby-head, this may take a while depending on your cpu(s)...

ruby-head - #fetching 
HEAD is now at 02035ba Merge branch 'trunk' of git://github.com/ruby/ruby into trunk

From github.com:andhapp/ruby
 * branch            trunk      -> FETCH_HEAD
Already up-to-date.
Copying from repo to src path...
ruby-head - #configuring 
ruby-head - #compiling 
ruby-head - #installing 
Retrieving rubygems-1.8.10
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  243k  100  243k    0     0   456k      0 --:--:-- --:--:-- --:--:--  540k

Extracting rubygems-1.8.10 ...
Removing old Rubygems files...
-e:1: Use RbConfig instead of obsolete and deprecated Config.
Installing rubygems-1.8.10 for ruby-head ...
Installation of rubygems completed successfully.
ruby-head - adjusting #shebangs for (gem irb erb ri rdoc testrb rake).
ruby-head - #importing default gemsets (/Users/andhapp/.rvm/gemsets/)
Install of ruby-head - #complete 

</pre>

This line 'HEAD is now at 02035ba Merge branch 'trunk' of git://github.com/ruby/ruby into trunk' is the last commit message on my local ruby git repository.

This line 'From github.com:andhapp/ruby' reflects the fact that rvm is using my git repository and not ruby's repository and updating the local source to the latest before installing.

I decided to call the ruby installation ruby-head. You can call it anything you fancy. 

Here's the version on my machine now:

<pre>
~/.rvm/src$ rvm use ruby-head
Using /Users/andhapp/.rvm/gems/ruby-head
~/.rvm/src$ ruby -v
ruby 2.0.0dev (2011-12-03 trunk 33936) [x86_64-darwin10.8.0]
</pre>


Awesome!


PS: I am sure there are other details about RVM's installation procedure that I have missed out and Wayne or Micheal will be kind enough to enlighten me.



