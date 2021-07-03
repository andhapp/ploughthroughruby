--- 
layout: post
title: Install pg and mysql gems
date_string: 22 February 2010
---


This is not entirely realted to ruby but if you ever program with ruby you will find yourself using pg and mysql gems and the issue is how exactly do I install them. This mini-post (rather tumble) is just to make a note of this. Run the following in Teerminal.

PostgreSql

<pre>
  export PATH=/usr/local/pgsql/bin:${PATH}
  gem install pg
</pre>

MySql

<pre>
  export PATH=/usr/local/mysql/bin:${PATH}
  gem install mysql
</pre>

Also, please note that you should have postgres and mysql installed on your machine. 
