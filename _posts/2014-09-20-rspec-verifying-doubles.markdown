---
layout: post
title: RSpec verifying doubles
date_string: 20 September 2014
--- 

RSpec 3 has been full of some good stuff and I have full admiration for
the people behind it. Even the upgrade process was well thought out
keeping in mind the end users. As developers, we are used to handle poor
upgrade process pretty well, but RSpec totally changed my opinion.

Whilst [merging pull request for TextRazor](https://github.com/andhapp/textrazor/pull/4), I decided to upgrade the gem
to RSpec3. I was meant to do that for sometime anyways, and the pull
request opened up the perfect opportunity for it. I stumbled upon a very
interesting new feature in RSpec3, called [verifying doubles](https://relishapp.com/rspec/rspec-mocks/v/3-0/docs/verifying-doubles/using-an-instance-double). This
functionality makes [rspec-fire](https://github.com/xaviershay/rspec-fire) totally obsolete. It verifies that any
methods being stubbed would be present on the instance of the class
being stubbed and also the number of argument the method accepts. This
is pretty cool. I always used rspec-fire to make sure that my stubbed
method existed on the class. In the light of these updates, I removed
[rspec-fire as a dependency from TextRazor](https://github.com/andhapp/textrazor/commit/48aeff496be89c7433dadfbbedd3e1d3e4375b64). Makes it even more
lightweight.

Thanks again to RSpec team!
