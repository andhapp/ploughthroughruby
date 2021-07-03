
---
layout: post
title: Improve Bundler CLI
date_string: 29 August 2016
---

Learn another programming language.

Learn from another programming ecosystem.

Learn from another programming language's tools and bring it back to the language you love.

Fact is, I love Ruby!

However, I've been spending a lot of time with Node.js lately. NPM provides a nice way to install
any new packages straight from the command line, like:

```
npm install react --save
```

I like this convenience.

With an intention to improve Ruby's ecosystem and tools, I would like to bring this to Ruby.

So, I've added a [new issue](https://github.com/bundler/bundler/issues/4932) to Bundler. Let's see what others feel about it.

**Update - 31 August 2016**

I had a couple of responses for my Bundler issue and it turns out there is indeed a way to add gems via bundler's CLI.

You can use the `inject` command like this:

```
bundle inject pg 0.18.4
```

You have to specify the exact version that you want to add though.

Next version of Bundler is going one better and will expose `add` command that will add the gem without needing a version number.
