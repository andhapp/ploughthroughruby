---
layout: post
title: Setting Up Chrome Selenium driver for Capybara when using chrome canary on a Mac
date_string: 31 December 2014
--- 

We have been adding Rspec + Capybara to [Suggestion.io](https://suggestion.io) 
to ensure we don't create any regression bugs. There are plenty of resources 
online to set-up Capybara to use Selenium's Chrome driver (instead of Firefox). 

### But, what if you are using Chrome Canary as your browser? 

You would probably see the following error: 

<pre>
Selenium::WebDriver::Error::UnknownError: unknown error: cannot find Chrome binary
</pre>

There are two ways to fix this issue:

### Solution 1 - Download Chrome

Whilst, searching for the solution, I ended up on [ChromeDriver's wiki](https://code.google.com/p/selenium/wiki/ChromeDriver). 
It clearly states that Chrome driver expects the Chrome binary to be in:

<pre>
/Applications/Google\ Chrome.app/Contents/MacOS/Google\ Chrome
</pre>

That's exactly where Chrome is installed on a Mac, so, to fix this issue
just download Chrome.

### Solution 2 - Pass the location of Chrome Canary's binary to Selenium Chrome Driver via Capybara

Downloading Chrome just for the sake of passing specs doesn't make
sense. Googling revealed that there's something called 'ChromeOptions', but, 
how the hell do I pass that option from Capybara, so that it get's passed 
correctly to Selenium Chrome driver. After, trawling through the
capybara and selenium-webdriver source, I found a way to pass the location 
of Chrome Canary as the binary. Here's how:

<pre>
Capybara.register_driver :chrome do |app|
  Capybara::Selenium::Driver.new(app, 
    browser: :chrome, 
    desired_capabilities: {
      "chromeOptions" => {
        "binary" => '/Applications/Google Chrome Canary.app/Contents/MacOS/Google Chrome Canary' 
      } 
    })
end
</pre>

The 'binary' option specifies the location of Chrome Canary's binary on
your Mac.

That was a couple of hours well spent. Hope it helps!
