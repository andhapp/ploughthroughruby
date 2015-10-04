---
layout: post
title: Rebooting an old gem
date_string: 04 October 2015
--- 

Novelty of writing a gem has worn off. Back in the days when Rails had
just come out, writing a gem (or a plugin) was an achievement in itself.

What has a gem got to do with Rails? You write ruby gems and rails is
just another gem, no? 

Correct!

It has nothing to do with Rails but my Ruby adventure began with Rails
and I for one give the credit where it's due, without a shadow of doubt.

#### History

Anyways, around 4 years ago, I created a gem called [is_bot](https://github.com/andhapp/is_bot). It offers some spam protection for web forms. I can't even remember the project I used it on back then.
However, recently we've been marketing [Suggestion.io](https://www.suggestion.io/) and encountered a lot of spam sign ups and decided to fix the issue.

#### Why not just use a captcha?

I hate asking prospective clients to fill in yet another field. You want
to make it easier not difficult to sign up. is_bot is different. It just
adds a invisible text field making it hidden from the actual users. Time
to get one back on the damn bots!

#### Why reboot? Why not use a Rails 4 gem?

I looked at few existing gems but none worked nicely. It was time to
reboot is_bot. Back then it was written for Rails 3 so had to upgrade it
for Rails 4 APIs which was a bit of a pain since it's hard to find what
changed from Rails 3 to Rails 4, easily. Reading through Rails source
code and looking at some of the other gems got us through.

#### Technology is flying...

I also took this opportunity to change a few more things...I say a few,
but so much has changed, hasn't it?

* Replaced Jeweler with Bundler as a gem to manage my ruby gem. Just
  find it easier to use.
* Started using semantic versioning. Makes perfect sense for open source project.
* Upgraded to latest RSpec.
* Replaced `.rvmrc` to `.ruby-gemset` and `.ruby-version`.

It was a bit of a work, but in the end all the efforts paid off.
